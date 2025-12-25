# Guide - Terraform Migration

> **Last Updated**: 2025-10-31 by Keming He

Essential workflows for diagnosing and executing state migrations when refactoring existing Terraform projects.

> [!NOTE]
>
> - **Scope**: Refactoring existing Terraform infrastructure only, not initial deployments
> - **Provider-agnostic**: Applicable to any cloud provider or service
> - **Official docs**:
>   - [Terraform State](https://developer.hashicorp.com/terraform/language/state)
>   - [Refactoring Modules](https://developer.hashicorp.com/terraform/language/modules/develop/refactoring)

## Table of Contents

- [Guide - Terraform Migration](#guide---terraform-migration)
  - [Table of Contents](#table-of-contents)
  - [Understanding State Addresses](#understanding-state-addresses)
  - [Diagnosing Migration Needs](#diagnosing-migration-needs)
    - [Static Code Analysis](#static-code-analysis)
    - [Using Terraform Plan](#using-terraform-plan)
  - [Changes Requiring Migration](#changes-requiring-migration)
    - [Module Instance Rename](#module-instance-rename)
    - [Resource Name Change](#resource-name-change)
    - [Iteration Key Changes](#iteration-key-changes)
  - [Changes Not Requiring Migration](#changes-not-requiring-migration)
    - [Module Source Path](#module-source-path)
    - [Variable Names and Values](#variable-names-and-values)
    - [Resource Attributes](#resource-attributes)
  - [Migration Strategies](#migration-strategies)
    - [State Move Command](#state-move-command)
    - [Import After Remove](#import-after-remove)
    - [Moved Block Declaration](#moved-block-declaration)
  - [Case Studies](#case-studies)
    - [Module Reorganization](#module-reorganization)
    - [Resource Refactoring](#resource-refactoring)
  - [Best Practices](#best-practices)

## Understanding State Addresses

Terraform tracks infrastructure through state addresses that map configuration to real resources.

**State address format**:

```text
module.<instance_name>.resource_type.resource_name[resource_key]
```

**Example**:

```text
module.database.aws_db_instance.primary
module.storage.aws_s3_bucket.data["production"]
```

**Critical principle**: Changes to state addresses make Terraform treat resources as new, triggering destroy and recreate operations.

**What affects state addresses**:

- Module instance names (`module "name"`)
- Resource names (`resource "type" "name"`)
- `for_each` keys or `count` indices

**What DOES NOT affect state addresses**:

- Module source paths (`source = "path"`)
- Variable names (`var.name`)
- Variable values or resource attributes

> [↑ Back to Table of Contents](#table-of-contents)

---

## Diagnosing Migration Needs

Determine if code changes require state migration using static analysis and runtime checks.

### Static Code Analysis

Review code changes against state address components.

```bash
# List current state addresses
terraform state list

# Compare with planned changes
# Ask: Do my changes modify module names, resource names, or for_each keys?
```

**Decision table**:

| Action | Migration required |
| :--- | :---: |
| Renaming `module "old"` to `module "new"` | **YES** |
| Changing `resource "type" "old"` to `resource "type" "new"` | **YES** |
| Modifying `for_each` keys | **YES** |
| Updating module `source` path | NO |
| Renaming variables | NO |

### Using Terraform Plan

```bash
# Generate plan to identify unintended changes
terraform plan

# Safe output shows updates to existing resources
# ~ update in-place

# Warning signs indicating migration need
# -/+ destroy and then create replacement
```

**If you see destroy/create for existing resources you intended to keep**, stop and perform state migration.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Changes Requiring Migration

These modifications alter state addresses and require explicit state management.

### Module Instance Rename

Changing module instance name breaks the state address mapping.

```terraform
# BEFORE
module "legacy_vpc" {
  source = "./modules/networking"
  cidr   = "10.0.0.0/16"
}

# AFTER
module "vpc" {
  source = "./modules/networking"
  cidr   = "10.0.0.0/16"
}
```

**Impact**: All resources in module appear as new to Terraform.

**See**: [Migration Strategies - State Move Command](#state-move-command)

### Resource Name Change

Renaming resources inside modules creates new state addresses.

```terraform
# BEFORE (modules/networking/main.tf)
resource "aws_vpc" "main_vpc" {
  cidr_block = var.cidr
}

# AFTER
resource "aws_vpc" "network" {
  cidr_block = var.cidr
}
```

**Impact**: Terraform plans to destroy old VPC and create new one with identical configuration.

**See**: [Migration Strategies - State Move Command](#state-move-command)

### Iteration Key Changes

Modifying `for_each` keys or switching between `count` and `for_each` changes resource addressing.

```terraform
# BEFORE
resource "aws_s3_bucket" "data" {
  for_each = toset(var.bucket_names)
  bucket   = each.value
}

# AFTER - different key structure
resource "aws_s3_bucket" "data" {
  for_each = { for b in var.buckets : b.name => b }
  bucket   = each.value.name
}
```

**Impact**: State addresses change from `aws_s3_bucket.data["bucket-name"]` to potentially different keys.

**See**: [Migration Strategies - Import After Remove](#import-after-remove)

> [↑ Back to Table of Contents](#table-of-contents)

---

## Changes Not Requiring Migration

These modifications preserve state addresses and apply safely.

### Module Source Path

Source paths are references to code location, not part of state identity.

```terraform
# BEFORE
module "vpc" {
  source = "./modules/networking"
  cidr   = "10.0.0.0/16"
}

# AFTER - relocated module
module "vpc" {
  source = "./infrastructure/modules/networking"
  cidr   = "10.0.0.0/16"
}
```

**State address unchanged**: `module.vpc.aws_vpc.network`

**Action**: Update source paths in consuming modules only.

### Variable Names and Values

Variables are configuration inputs, not state identifiers.

```terraform
# BEFORE
variable "vpc_cidr" {
  type = string
}

# AFTER
variable "network_cidr" {
  type = string
}
```

**Action**: Update all variable references in code. Terraform will update resource attributes in-place if values differ.

### Resource Attributes

Changing resource properties updates infrastructure without migration.

```terraform
# BEFORE
resource "aws_instance" "web" {
  instance_type = "t2.micro"
  ami           = "ami-12345"
}

# AFTER
resource "aws_instance" "web" {
  instance_type = "t2.small"
  ami           = "ami-67890"
}
```

**Action**: Run `terraform apply` to update resources. Terraform handles attribute changes automatically.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Migration Strategies

Execute state migrations safely with these techniques.

### State Move Command

Rename resources in state to match new code structure.

```bash
# Backup state first
terraform state pull > backup.tfstate

# Move single resource
terraform state mv \
  'module.legacy_vpc.aws_vpc.main_vpc' \
  'module.vpc.aws_vpc.network'

# Move entire module
terraform state mv \
  'module.legacy_vpc' \
  'module.vpc'

# Verify no unintended changes
terraform plan
```

**Use for**: Module/resource renames, straightforward refactoring

**Docs**: [`terraform state mv`](https://developer.hashicorp.com/terraform/cli/commands/state/mv)

### Import After Remove

Remove resources from state, update code, then re-import existing infrastructure.

```bash
# Backup state
terraform state pull > backup.tfstate

# Remove from state (infrastructure unchanged)
terraform state rm 'module.legacy_vpc'

# Update code with new names

# Import existing resources
terraform import 'module.vpc.aws_vpc.network' vpc-abc123

# Verify
terraform plan
```

**Use for**: Complex refactors with many resources, iteration key restructuring

**Docs**: [`terraform import`](https://developer.hashicorp.com/terraform/cli/commands/import)

### Moved Block Declaration

Declare refactoring intentions in code for Terraform to handle migration automatically.

```terraform
# Add to configuration
moved {
  from = module.legacy_vpc
  to   = module.vpc
}

# Terraform handles state migration on next apply
```

**Use for**: Terraform 1.1+, team-wide refactoring coordination, repeatable migrations

**Benefits**: Version-controlled migration history, automatic state updates

**Docs**: [Refactoring with moved blocks](https://developer.hashicorp.com/terraform/language/modules/develop/refactoring#move-a-resource-or-module)

> [↑ Back to Table of Contents](#table-of-contents)

---

## Case Studies

Real-world scenarios demonstrating diagnosis and migration workflows.

### Module Reorganization

**Scenario**: Restructuring modules from flat to hierarchical organization.

**Original structure**:

```terraform
module "vpc" {
  source = "./modules/vpc"
}

module "subnets" {
  source = "./modules/subnets"
}
```

**New structure**:

```terraform
module "networking" {
  source = "./modules/networking"
  # Internally contains vpc and subnet resources
}
```

**Diagnosis**:

- Module instance names changed: `vpc`, `subnets` → `networking`
- State addresses will break
- Migration required

**Solution**: State move commands

```bash
terraform state pull > backup.tfstate

# Move resources to new module structure
terraform state mv 'module.vpc.aws_vpc.main' 'module.networking.aws_vpc.main'
terraform state mv 'module.subnets' 'module.networking.module.subnets'

terraform plan  # Verify no changes
```

### Resource Refactoring

**Scenario**: Converting individual resources to `for_each` loop for maintainability.

**Original configuration**:

```terraform
resource "aws_s3_bucket" "data_dev" {
  bucket = "data-dev"
}

resource "aws_s3_bucket" "data_prod" {
  bucket = "data-prod"
}
```

**New configuration**:

```terraform
resource "aws_s3_bucket" "data" {
  for_each = toset(["dev", "prod"])
  bucket   = "data-${each.value}"
}
```

**Diagnosis**:

- Resource names changing: `data_dev`, `data_prod` → `data`
- New iteration keys introduced
- State addresses incompatible
- Migration required

**Solution**: Import after remove

```bash
terraform state pull > backup.tfstate

# Remove old resources from state
terraform state rm 'aws_s3_bucket.data_dev'
terraform state rm 'aws_s3_bucket.data_prod'

# Import under new structure
terraform import 'aws_s3_bucket.data["dev"]' data-dev
terraform import 'aws_s3_bucket.data["prod"]' data-prod

terraform plan  # Verify no changes
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Best Practices

**Before refactoring**:

- Backup state: `terraform state pull > backup.tfstate`
- Document current addresses: `terraform state list > current-resources.txt`
- Test in non-production environment first

**During migration**:

- Migrate one resource at a time to limit blast radius
- Verify after each move: `terraform plan` should show no changes for migrated resources
- Keep migration commands documented for audit trail

**Choosing strategies**:

- **moved block** (Terraform 1.1+): Best for coordinated team refactoring
- **state mv**: Fast for simple renames, individual resources
- **import after remove**: Complex restructuring, many resources

**After migration**:

- Run `terraform plan` to confirm no unexpected changes
- Backup final state: `terraform state pull > post-migration.tfstate`
- Update documentation with any API changes

> [↑ Back to Table of Contents](#table-of-contents)

---

> Terraform Migration Guide v1.0.0 - KemingHe/common-devx
