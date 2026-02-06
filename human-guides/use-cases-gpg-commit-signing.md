# Use Cases - GPG Commit Signing

> **Last Updated**: 2026-02-06 by Keming He

## Platform

> [!IMPORTANT]
>
> This guide is for **macOS / Linux** users with POSIX-compatible shell (sh, bash, zsh).
>
> For **Windows** users: See [GitHub: Managing commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification).

Sign commits with GPG keys for verified badges on GitHub.

## Table of Contents

- [Use Cases - GPG Commit Signing](#use-cases---gpg-commit-signing)
  - [Platform](#platform)
  - [Table of Contents](#table-of-contents)
  - [Why Sign Commits?](#why-sign-commits)
  - [Check for Existing Keys](#check-for-existing-keys)
  - [Generate New Key](#generate-new-key)
    - [Install GPG](#install-gpg)
    - [Generate Key](#generate-key)
    - [Get Key ID](#get-key-id)
  - [Add Key to GitHub](#add-key-to-github)
    - [Export Public Key](#export-public-key)
    - [Add to GitHub](#add-to-github)
  - [Configure Git](#configure-git)
    - [Set Signing Key](#set-signing-key)
    - [Enable Auto-Signing](#enable-auto-signing)
    - [Configure TTY for Passphrase Prompt](#configure-tty-for-passphrase-prompt)
  - [Sign Commits](#sign-commits)
    - [Signing Behavior](#signing-behavior)
    - [Skip Signing](#skip-signing)
    - [Verify Signature](#verify-signature)
  - [Troubleshooting](#troubleshooting)
    - [Lock File Issues](#lock-file-issues)

## Why Sign Commits?

- **Verified badge**: Signed commits display a "Verified" badge on GitHub, proving the commit came from you
- **Expiration/revocation**: Unlike SSH signing, GPG keys can expire or be revoked, giving you more control over key lifecycle

> [↑ Back to Table of Contents](#table-of-contents)

---

## Check for Existing Keys

```shell
gpg --list-secret-keys --keyid-format=long
```

If you see keys listed, note the key ID (see [Get Key ID](#get-key-id) for how to read the output). If no keys exist, proceed to generate a new one.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Generate New Key

### Install GPG

```shell
# macOS
brew install gnupg

# Ubuntu/Debian
sudo apt-get install gnupg
```

### Generate Key

```shell
gpg --full-generate-key
```

When prompted:

1. Select **RSA and RSA** (default)
2. Key size: **4096** bits
3. Expiration: Choose based on your security needs (recommended: 1-3 years)
4. Enter your **GitHub email address** as the user ID
5. Set a secure passphrase

> [!TIP]
>
> **Setting an expiration is good practice** - it forces periodic key rotation. When a key expires:
>
> - New signatures fail until you extend or replace the key
> - Old signatures remain valid (GitHub still shows "Verified")
> - To extend: `gpg --edit-key YOUR_KEY_ID` → `expire` → set new date → `save`

### Get Key ID

After generation, list your keys:

```shell
gpg --list-secret-keys --keyid-format=long
```

Output looks like:

```shell
sec   rsa4096/ABCDEF1234567890 2026-02-06 [SC] [expires: 2029-02-05]
      1234567890123456789012345678901234567890
uid                 [ultimate] Your Name <your-email@github.com>
ssb   rsa4096/FEDCBA0987654321 2026-02-06 [E] [expires: 2029-02-05]
```

**Output lines explained**:

| Line | Meaning |
| :--- | :--- |
| `sec` | **Sec**ret key - your main signing key. `rsa4096` = algorithm and key size. `[SC]` = Sign + Certify capabilities |
| (indented) | Fingerprint - full 40-character hex identifier |
| `uid` | **U**ser **ID** - your identity (name + email). `[ultimate]` = you fully trust this key |
| `ssb` | **S**ecret **s**u**b**key - typically for encryption. `[E]` = Encrypt capability |

**Key identifier types** (for export and signing config):

> [!TIP]
>
> **Use long ID or fingerprint** - never short ID. Long ID is readable and sufficient for personal use. Fingerprint is more explicit - prefer it in shared/organizational contexts.

| Type | Length | Example | Where | Collision risk |
| :--- | :--- | :--- | :--- | :--- |
| Short ID | 8 hex | `34567890` | Last 8 chars of long ID | High - avoid |
| Long ID | 16 hex | `ABCDEF1234567890` | After `rsa4096/` on `sec` line | Low |
| Fingerprint | 40 hex | `1234567890123456789012345678901234567890` | Full line below `sec` | None |

> [↑ Back to Table of Contents](#table-of-contents)

---

## Add Key to GitHub

### Export Public Key

Use your long ID or fingerprint from [Get Key ID](#get-key-id):

```shell
gpg --armor --export ABCDEF1234567890
# or with fingerprint:
gpg --armor --export 1234567890123456789012345678901234567890
```

Copy the entire output, including `-----BEGIN PGP PUBLIC KEY BLOCK-----` and `-----END PGP PUBLIC KEY BLOCK-----`.

### Add to GitHub

1. Go to [**GitHub Settings**](https://github.com/settings/) > [**SSH and GPG keys**](https://github.com/settings/keys)
2. Click **New GPG key**
3. Paste your public key
4. Click **Add GPG key**

> [↑ Back to Table of Contents](#table-of-contents)

---

## Configure Git

> [!NOTE]
>
> **One GPG key per identity.** If you have multiple Git identities (work/personal), see [Multiple Identities](./use-cases-git.md#multiple-identities) for directory-based auto-switching.

### Set Signing Key

Use your long ID or fingerprint from [Get Key ID](#get-key-id):

```shell
git config --global user.signingkey ABCDEF1234567890
# or with fingerprint:
git config --global user.signingkey 1234567890123456789012345678901234567890
```

### Enable Auto-Signing

```shell
git config --global commit.gpgsign true
```

### Configure TTY for Passphrase Prompt

Add to your shell profile (`~/.bashrc`, `~/.zshrc`, etc.):

```shell
export GPG_TTY=$(tty)
```

Then reload your shell:

```shell
source ~/.zshrc   # or ~/.bashrc
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Sign Commits

### Signing Behavior

If you enabled auto-signing in [Configure Git](#configure-git), all commits are signed automatically:

```shell
git commit -m "your commit message"    # Automatically signed
```

To manually sign a single commit (if auto-signing is disabled):

```shell
git commit -S -m "your commit message"
```

### Skip Signing

To skip signing for a single commit:

```shell
git commit --no-gpg-sign -m "your message"
```

### Verify Signature

```shell
git log --show-signature -1
```

If configured correctly, you'll see signature verification info in the output.

> [↑ Back to Table of Contents](#table-of-contents)

---

## Troubleshooting

### Lock File Issues

**Symptom**:

```shell
error: gpg failed to sign the data
fatal: failed to write commit object
```

Running `gpg --list-secret-keys --keyid-format=long` hangs or shows `waiting for lock`.

**Solution**:

```shell
# 1. Kill GPG agent
gpgconf --kill gpg-agent

# 2. Remove lock files
find ~/.gnupg -name "*.lock" -delete

# 3. Verify fix
gpg --list-secret-keys --keyid-format=long    # Should respond immediately
echo "test" | gpg --clearsign                 # Should sign successfully

# 4. Retry your commit
```

**Prevention**: Lock files occur when GPG processes are interrupted. Run `gpgconf --kill gpg-agent` periodically to prevent stale processes.

If the issue persists and you need to commit urgently, see [Skip Signing](#skip-signing).

> [↑ Back to Table of Contents](#table-of-contents)

---

> Use Cases - GPG Commit Signing v1.0.0 - KemingHe/common-devx
