# Diagnosis - Terraform State Migration

> **Last Updated**: 2026-02-06 by Keming He

## Platform

> [!IMPORTANT]
>
> **Platform-agnostic** - Terraform CLI works identically on macOS, Linux, and Windows.

Diagnose and execute state migrations when refactoring Terraform projects.

## Table of Contents

- [Diagnosis - Terraform State Migration](#diagnosis---terraform-state-migration)
  - [Platform](#platform)
  - [Table of Contents](#table-of-contents)
  - [When Migration Is Needed](#when-migration-is-needed)
  - [Diagnose with Terraform Plan](#diagnose-with-terraform-plan)
  - [Migration Strategies](#migration-strategies)
    - [Strategy 1: State Move](#strategy-1-state-move)
    - [Strategy 2: Moved Block (Terraform 1.1+)](#strategy-2-moved-block-terraform-11)
    - [Strategy 3: Import After Remove](#strategy-3-import-after-remove)
  - [Examples](#examples)
    - [Module Rename](#module-rename)
    - [Resource Rename](#resource-rename)
    - [Convert to for\_each](#convert-to-for_each)
  - [Best Practices](#best-practices)
  - [References](#references)

## When Migration Is Needed

State addresses follow this format:

```text
module.<instance_name>.resource_type.resource_name[key]
```

| Change | Migration Required |
| :--- | :---: |
| Rename `module "old"` to `module "new"` | **Yes** |
| Rename `resource "type" "old"` to `"new"` | **Yes** |
| Change `for_each` keys | **Yes** |
| Change module `source` path | No |
| Rename variables | No |
| Change resource attributes | No |

**Rule**: If the state address changes, migration is required.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Diagnose with Terraform Plan

```shell
terraform plan
```

| Plan Output | Meaning |
| :--- | :--- |
| `~ update in-place` | Safe - no migration needed |
| `-/+ destroy and create` | **Stop** - migration needed |

If you see destroy/create for resources you want to keep, perform state migration before applying.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Migration Strategies

### Strategy 1: State Move

Best for simple renames.

```shell
# Backup first
terraform state pull > backup.tfstate

# Move resource
terraform state mv 'module.old.aws_vpc.main' 'module.new.aws_vpc.main'

# Move entire module
terraform state mv 'module.old' 'module.new'

# Verify
terraform plan                    # Should show no changes
```

### Strategy 2: Moved Block (Terraform 1.1+)

Best for team coordination and version-controlled migrations.

```terraform
moved {
  from = module.old
  to   = module.new
}
```

Terraform handles migration automatically on next apply.

### Strategy 3: Import After Remove

Best for complex restructuring.

```shell
# Backup
terraform state pull > backup.tfstate

# Remove from state (infrastructure unchanged)
terraform state rm 'aws_s3_bucket.old'

# Update code, then import
terraform import 'aws_s3_bucket.new["key"]' bucket-id

# Verify
terraform plan
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Examples

### Module Rename

```shell
# module.legacy_vpc -> module.vpc
terraform state mv 'module.legacy_vpc' 'module.vpc'
```

### Resource Rename

```shell
# aws_vpc.main_vpc -> aws_vpc.network
terraform state mv 'module.vpc.aws_vpc.main_vpc' 'module.vpc.aws_vpc.network'
```

### Convert to for_each

```shell
# Individual resources -> for_each loop
terraform state rm 'aws_s3_bucket.data_dev'
terraform state rm 'aws_s3_bucket.data_prod'

# After updating code
terraform import 'aws_s3_bucket.data["dev"]' data-dev
terraform import 'aws_s3_bucket.data["prod"]' data-prod
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Best Practices

**Before**:

- Backup: `terraform state pull > backup.tfstate`
- Document: `terraform state list > current.txt`
- Test in non-production first

**During**:

- One resource at a time
- Verify after each move: `terraform plan` should show no changes

**After**:

- Confirm: `terraform plan` shows no unexpected changes
- Backup final state

**Strategy Selection**:

| Situation | Use |
| :--- | :--- |
| Simple rename | `state mv` |
| Team refactoring | `moved` block |
| Complex restructuring | Import after remove |

> [↑ Back to Table of Contents](#table-of-contents)

---

## References

- [Terraform State](https://developer.hashicorp.com/terraform/language/state)
- [Refactoring with moved blocks](https://developer.hashicorp.com/terraform/language/modules/develop/refactoring)
- [`terraform state mv`](https://developer.hashicorp.com/terraform/cli/commands/state/mv)
- [`terraform import`](https://developer.hashicorp.com/terraform/cli/commands/import)

---

> Diagnosis - Terraform State Migration v2.0.1 - KemingHe/common-devx
