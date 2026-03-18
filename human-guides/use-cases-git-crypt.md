# Use Cases - [git-crypt](https://github.com/AGWA/git-crypt)

> **Last Updated**: 2026-03-18 by Keming He based on `git-crypt` [v0.8.0 release](https://github.com/AGWA/git-crypt/releases/tag/0.8.0)

## Platform

> [!IMPORTANT]
>
> This guide is for **macOS / Linux** users with POSIX-compatible shell (sh, bash, zsh).
>
> For **Windows** users: See [AGWA/git-crypt - INSTALL.md - Experimental Windows Support](https://github.com/AGWA/git-crypt/blob/master/INSTALL.md).

Transparent file encryption in Git repositories using GPG keys.

## Table of Contents

- [Use Cases - git-crypt](#use-cases---git-crypt)
  - [Platform](#platform)
  - [Table of Contents](#table-of-contents)
  - [Why Use git-crypt?](#why-use-git-crypt)
  - [Prerequisites](#prerequisites)
  - [Install git-crypt](#install-git-crypt)
  - [Initialize Repository](#initialize-repository)
  - [Configure Encryption Patterns](#configure-encryption-patterns)
    - [Basic Syntax](#basic-syntax)
    - [Pattern Examples](#pattern-examples)
    - [Critical: Exclusion Rule Order](#critical-exclusion-rule-order)
  - [Working with Encrypted Repos](#working-with-encrypted-repos)
    - [Clone and Unlock](#clone-and-unlock)
    - [Check Encryption Status](#check-encryption-status)
    - [Verify Encryption](#verify-encryption)
  - [Key Management](#key-management)
    - [Export GPG Key for Backup](#export-gpg-key-for-backup)
    - [Adding Collaborators](#adding-collaborators)
    - [Removing Access](#removing-access)
  - [Encrypt Existing Files](#encrypt-existing-files)
  - [Multi-Branch Workflows](#multi-branch-workflows)
  - [Troubleshooting](#troubleshooting)
    - [Unlock Fails with GPG Error](#unlock-fails-with-gpg-error)
    - [Files Not Being Encrypted](#files-not-being-encrypted)
    - [Merge Conflicts in Encrypted Files](#merge-conflicts-in-encrypted-files)
  - [Known Limitations](#known-limitations)
  - [Related Guides](#related-guides)

## Why Use git-crypt?

- **Transparent encryption**: Encrypt files automatically on commit, decrypt on checkout - no manual steps
- **AES-256 encryption**: Industry-standard symmetric encryption for file contents
- **Works with existing workflows**: Use normal git commands - clone, pull, push, diff all work seamlessly
- **GPG-based access control**: Grant access using GPG public keys - no shared secrets to manage

> [↑ Back to Table of Contents](#table-of-contents)

---

## Prerequisites

> [!IMPORTANT]
>
> **GPG key required.** git-crypt uses GPG keys to encrypt the repository's symmetric key. You need a GPG key with an encryption-capable subkey.

If you don't have a GPG key, see [Use Cases - GPG Commit Signing](./use-cases-gpg-commit-signing.md) to generate one.

**Verify your key has encryption capability**:

```shell
gpg --list-secret-keys --keyid-format=long
```

Look for `[E]` (Encrypt) capability in the output:

```shell
sec   rsa4096/ABCDEF1234567890 2026-02-06 [SC] [expires: 2029-02-05]
      1234567890123456789012345678901234567890
uid                 [ultimate] Your Name <your-email@example.com>
ssb   rsa4096/FEDCBA0987654321 2026-02-06 [E] [expires: 2029-02-05]
```

The `ssb` line with `[E]` indicates an encryption-capable subkey. If missing, you need to add one with `gpg --edit-key YOUR_KEY_ID` then `addkey`.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Install git-crypt

**macOS**:

```shell
brew install git-crypt
```

**Ubuntu/Debian**:

```shell
sudo apt-get install git-crypt
```

**Verify installation**:

```shell
git-crypt --version
```

Expected output: `git-crypt 0.8.0` (or similar version number).

> [↑ Back to Table of Contents](#table-of-contents)

---

## Initialize Repository

> [!NOTE]
>
> Initialize git-crypt in an existing Git repository. The repository must have at least one commit.

**Initialize git-crypt**:

```shell
git-crypt init
```

This creates a random AES-256 key stored in `.git/git-crypt/keys/default`.

**Add yourself as a trusted user**:

```shell
git-crypt add-gpg-user YOUR_GPG_KEY_ID
```

Use your long key ID or fingerprint from [Prerequisites](#prerequisites).

> [!TIP]
>
> This command automatically commits `.git-crypt/` files to the repository. These files contain the encrypted symmetric key - one copy per authorized GPG key.

**Verify setup**:

```shell
ls .git-crypt/
```

You should see `keys/` directory with your GPG-encrypted key file.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Configure Encryption Patterns

> [!WARNING]
>
> **Security: `.gitattributes` tampering risk.** git-crypt cannot be used securely unless the entire repository is protected against tampering. An attacker who can mutate your repository can alter the `.gitattributes` file to disable encryption. Use Git signed tags or commits to protect repository integrity.

Encryption patterns are defined in `.gitattributes` using Git's filter and diff attributes.

### Basic Syntax

```text
PATTERN filter=git-crypt diff=git-crypt
```

Where `PATTERN` is a gitignore-style glob pattern with _one critical exception_: specifying only a directory path like `/dir/` does NOT encrypt files beneath it. You _must_ use `dir/**` to encrypt entire directory trees.

### Pattern Examples

```text
# Encrypt all files in secrets/ directory
secrets/** filter=git-crypt diff=git-crypt

# Encrypt specific file types
*.key filter=git-crypt diff=git-crypt
*.pem filter=git-crypt diff=git-crypt

# Encrypt environment files
.env filter=git-crypt diff=git-crypt
.env.* filter=git-crypt diff=git-crypt

# Encrypt files with specific naming
**/credentials.json filter=git-crypt diff=git-crypt
**/secrets.yaml filter=git-crypt diff=git-crypt
```

### Critical: Exclusion Rule Order

> [!IMPORTANT]
>
> **Exclusion rules MUST be at the END of the file.** Git attributes use last-match-wins semantics. If you need to exclude files from encryption, place those rules after the encryption rules.

**Correct order**:

```text
# Encrypt everything in secrets/
secrets/** filter=git-crypt diff=git-crypt

# EXCEPTION: Do NOT encrypt the README (must be LAST)
secrets/README.md !filter !diff
```

**Incorrect order** (README would be encrypted):

```text
# This exclusion is overridden by the rule below - WRONG
secrets/README.md !filter !diff
secrets/** filter=git-crypt diff=git-crypt
```

The `.gitattributes` file itself should _never_ be encrypted - it must be readable to determine which files to decrypt.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Working with Encrypted Repos

### Clone and Unlock

When you clone a git-crypt repository, encrypted files appear as binary data until unlocked.

```shell
git clone git@github.com:username/repo.git # via SSH
# git clone https://github.com/username/repo.git # via HTTP
cd repo

# Unlock with your GPG key
git-crypt unlock
```

git-crypt automatically finds your GPG key if you were added as a trusted user.

### Check Encryption Status

```shell
# List all files and their encryption status
git-crypt status
```

Output shows which files are encrypted:

```shell
    encrypted: secrets/api-key.txt
    encrypted: .env
not encrypted: README.md
not encrypted: .gitattributes
```

### Verify Encryption

**Test that files are actually encrypted in the repository**:

```shell
# Lock the repository (re-encrypts files in working directory)
git-crypt lock

# View an "encrypted" file - should be binary garbage
cat secrets/api-key.txt

# Unlock to restore readable content
git-crypt unlock
```

**Verify encryption in git history**:

```shell
# Show raw blob content (should be encrypted)
git show HEAD:secrets/api-key.txt | head -c 100 | xxd
```

Encrypted content starts with `\x00GITCRYPT`.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Key Management

### Export GPG Key for Backup

> [!IMPORTANT]
>
> **Back up your GPG private key.** If you lose access to your GPG key, you lose access to the encrypted repository. There is **NO** recovery mechanism.

Export your private key for secure backup (e.g., password manager, offline storage):

```shell
# Export private key (includes encryption subkey)
gpg --armor --export-secret-keys YOUR_KEY_ID > private-key-backup.asc

# Export public key (for sharing with collaborators)
gpg --armor --export YOUR_KEY_ID > public-key.asc
```

Store `private-key-backup.asc` securely. Delete the file after importing to your backup location:

```shell
# macOS (BSD) - overwrite 3x before delete
rm -P private-key-backup.asc public-key.asc

# Linux (GNU) - overwrite before delete
shred -u private-key-backup.asc public-key.asc
```

### Adding Collaborators

To grant repository access to another user:

1. **Obtain their GPG public key**:

   ```shell
   # They export their public key
   gpg --armor --export THEIR_KEY_ID > collaborator-public.asc
   
   # You import it
   gpg --import collaborator-public.asc
   ```

2. **Add them to git-crypt**:

   ```shell
   git-crypt add-gpg-user THEIR_KEY_ID
   ```

3. **Push the changes** (auto-committed by git-crypt):

   ```shell
   git push
   ```

The collaborator can now clone and `git-crypt unlock` using their GPG key.

### Removing Access

> [!IMPORTANT]
>
> **git-crypt has no revocation mechanism.** Once someone has access, they can decrypt **ALL** historical commits forever. Removing their `.git-crypt/` key file only prevents future unlocks from new clones. Any user with an old clone and the old key can still decrypt all historical commits, even after re-initialization.

**To truly revoke access requires rotating all secrets**:

1. Rotate all secrets in the repository (API keys, passwords, certificates, etc.)
2. Re-initialize git-crypt with a new symmetric key
3. Re-add only authorized users
4. Force-push the new history (destructive operation)

Even after re-initialization, anyone with the old key can still access all historical commits in old clones. This is why secret rotation is critical, not just key rotation. See [Known Limitations](#known-limitations) for more details.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Encrypt Existing Files

If you add `.gitattributes` patterns for files already tracked in the repository, they are not automatically re-encrypted. You must force re-encryption.

**Force re-encryption of all files**:

```shell
git-crypt status -f
```

This re-stages files that should be encrypted based on current `.gitattributes` patterns.

**Commit the re-encrypted files**:

```shell
git add -A
git commit -m "chore(security): encrypt existing files with git-crypt"
```

Previous commits still contain unencrypted content - see [Known Limitations](#known-limitations) about retroactive encryption.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Multi-Branch Workflows

When working with multiple branches, encryption status can become inconsistent if branches have different `.gitattributes` configurations.

**Best practice**: Update `.gitattributes` on your `main`/default branch first, then rebase feature branches.

**If encryption patterns changed on main**:

```shell
# On your feature branch
git fetch origin
git rebase origin/main
```

**If files need re-encryption after rebase**:

```shell
# Remove files from index (keep working copy)
git rm --cached path/to/file

# Re-add to trigger encryption
git add path/to/file

# Commit the re-encrypted version
git commit --amend --no-edit
```

For complex Git workflows, see [Use Cases - Git](./use-cases-git.md).

> [↑ Back to Table of Contents](#table-of-contents)

---

## Troubleshooting

### Unlock Fails with GPG Error

**Symptom**:

```shell
Error: no GPG secret key available to unlock this repository
```

**Causes and fixes**:

1. **GPG key not imported**:

   ```shell
   gpg --list-secret-keys --keyid-format=long
   ```

   If your key is missing, import your backup: `gpg --import private-key-backup.asc`

2. **GPG agent not running**:

   ```shell
   gpgconf --kill gpg-agent
   gpg-agent --daemon
   git-crypt unlock
   ```

3. **You were never added as a trusted user**: Contact the repository owner to run `git-crypt add-gpg-user YOUR_KEY_ID`.

### Files Not Being Encrypted

**Symptom**: `git-crypt status` shows files as "not encrypted" that should be encrypted.

**Causes and fixes**:

1. **Pattern not matching**: Check `.gitattributes` syntax. Test with:

   ```shell
   git check-attr filter path/to/file
   ```

   Should output `path/to/file: filter: git-crypt`.

2. **Files committed before pattern was added**: Force re-encryption:

   ```shell
   git-crypt status -f
   git add -A
   git commit -m "chore: re-encrypt files"
   ```

3. **Exclusion rule overriding encryption**: Check rule order in `.gitattributes` - see [Critical: Exclusion Rule Order](#critical-exclusion-rule-order).

### Merge Conflicts in Encrypted Files

**Symptom**: Merge shows binary conflict markers in encrypted files.

**Fix**: Resolve by choosing one version entirely:

```shell
# Keep our version
git checkout --ours path/to/file
git add path/to/file

# Or keep their version
git checkout --theirs path/to/file
git add path/to/file
```

Manual merge of encrypted content is not possible - you must choose one side or re-create the file after unlocking.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Known Limitations

| Limitation | Description | Mitigation |
| :--- | :--- | :--- |
| No retroactive encryption | Encrypting a file does not encrypt its history. Previous commits remain unencrypted. | Retroactively encrypt files with [`git-crypt-retro`](https://github.com/KemingHe/git-crypt-retro) (new), or rewrite history with [`git-filter-repo`](https://github.com/newren/git-filter-repo) (mature), or start fresh. |
| File paths visible | Only file _contents_ are encrypted. File names and paths are visible to anyone. | Use generic names like `secrets/config.enc` instead of `secrets/aws-credentials.json`. |
| Metadata leakage | File sizes, modification times, and commit metadata are not hidden. | Accept this limitation or use a different solution for high-security needs. |
| No revocation | Removing a user's key file does not prevent access to previously cloned repositories. Anyone with old clones and old keys can decrypt all historical commits forever. | Rotate all secrets when removing users. Re-initialization only prevents future access, not historical access. |
| Binary diffs | Encrypted files show as binary - `git diff` is not useful. | Run `git-crypt unlock` before reviewing changes. |
| GUI incompatibility | Does not work reliably with some third-party Git GUIs like Atlassian SourceTree and GitHub for Mac. Files may be left unencrypted. | Use command-line Git or verify encryption status after GUI operations with `git-crypt status`. |
| Patch application | Encrypted files cannot be patched with `git-apply` unless the patch itself is encrypted. | Use `git diff --no-textconv --binary` to generate encrypted patches, or apply plaintext patches outside Git using the `patch` command. |

> [↑ Back to Table of Contents](#table-of-contents)

---

## Related Guides

- [Use Cases - GPG Commit Signing](./use-cases-gpg-commit-signing.md) - Generate and manage GPG keys
- [Use Cases - Git](./use-cases-git.md) - Git workflows, rebasing, and history rewriting
- [Use Cases - SSH Authentication](./use-cases-ssh-authentication.md) - SSH key setup for Git hosting

> [↑ Back to Table of Contents](#table-of-contents)
