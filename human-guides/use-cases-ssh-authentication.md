# Use Cases - SSH Authentication

> **Last Updated**: 2026-02-16 by Keming He

## Platform

> [!IMPORTANT]
>
> This guide is for **macOS / Linux** users with POSIX-compatible shell (sh, bash, zsh).
>
> For **Windows** users: See [GitHub: Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

Authenticate to Git hosting services and remote servers using SSH keys.

## Table of Contents

- [Use Cases - SSH Authentication](#use-cases---ssh-authentication)
  - [Platform](#platform)
  - [Table of Contents](#table-of-contents)
  - [Why Use SSH Keys?](#why-use-ssh-keys)
  - [Check for Existing Keys](#check-for-existing-keys)
  - [Generate New Key](#generate-new-key)
    - [Generate Key](#generate-key)
    - [Add to ssh-agent](#add-to-ssh-agent)
  - [Use Case: Git Hosting](#use-case-git-hosting)
    - [Copy Public Key](#copy-public-key)
    - [Add Key to GitHub](#add-key-to-github)
    - [URL Rewriting](#url-rewriting)
    - [Test Connection](#test-connection)
  - [Use Case: Remote Servers](#use-case-remote-servers)
    - [Add Key to Host](#add-key-to-host)
    - [Connect](#connect)
    - [File Transfer (SCP)](#file-transfer-scp)
  - [Troubleshooting](#troubleshooting)
    - [Permission Denied](#permission-denied)
    - [Agent Issues](#agent-issues)
    - [Managing Known Hosts](#managing-known-hosts)

## Why Use SSH Keys?

- **Passwordless auth**: No prompts for git operations or server logins
- **More secure**: Key-based authentication is stronger than passwords
- **One setup, multiple uses**: Same key works for Git hosting, servers, and file transfer

> [↑ Back to Table of Contents](#table-of-contents)

---

## Check for Existing Keys

```shell
ls -la ~/.ssh
```

Look for files like `id_ed25519` and `id_ed25519.pub` (or `id_rsa`/`id_rsa.pub`). If you have a key pair, you can skip to [Add to ssh-agent](#add-to-ssh-agent).

> [↑ Back to Table of Contents](#table-of-contents)

---

## Generate New Key

### Generate Key

**Ed25519** (recommended - smaller, faster, more secure):

```shell
ssh-keygen -t ed25519 -C "your-email@example.com"
```

When prompted:

1. Press **Enter** to accept the default file location (`~/.ssh/id_ed25519`)
2. Enter a passphrase (optional but recommended)

> [!TIP]
>
> **Passphrase adds security** - if your private key is compromised, the attacker still needs the passphrase. The ssh-agent caches it so you don't type it repeatedly.

For legacy systems that don't support Ed25519:

```shell
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

### Add to ssh-agent

The ssh-agent caches your key so you don't enter the passphrase repeatedly.

```shell
# Start agent (usually auto-started on macOS)
eval "$(ssh-agent -s)"

# Add key
ssh-add ~/.ssh/id_ed25519

# macOS - Use keychain for persistence across reboots
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

# macOS - Add to `~/.ssh/config` so keys auto-load:
# Host *
#   AddKeysToAgent yes
#   UseKeychain yes
#   IdentityFile ~/.ssh/id_ed25519
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Use Case: Git Hosting

### Copy Public Key

```shell
# Display public key (copy the output)
cat ~/.ssh/id_ed25519.pub

# macOS: copy directly to clipboard
pbcopy < ~/.ssh/id_ed25519.pub
```

### Add Key to GitHub

**GitHub**:

1. Go to [**GitHub Settings**](https://github.com/settings/) > [**SSH and GPG keys**](https://github.com/settings/keys)
2. Click **New SSH key**
3. Title: descriptive name (e.g., "[Device Name] [YYYY]")
4. Key type: **Authentication Key**
5. Paste your public key
6. Click **Add SSH key**

### URL Rewriting

> [!TIP]
>
> **Use HTTPS URLs but authenticate via SSH** - clone commands from GitHub's UI work as-is, no manual URL conversion needed.

```shell
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

With this config:

```shell
# This HTTPS URL from GitHub's UI...
git clone https://github.com/username/repo.git

# ...automatically uses SSH authentication
# (Git rewrites it to git@github.com:username/repo.git)
```

> [!NOTE]
>
> This rule is applied silently. If you later forget it is set, HTTPS clone URLs will fail with SSH errors like `Permission denied (publickey)`. See [Git guide - URL Rewriting Issues](./use-cases-git.md#url-rewriting-issues) for diagnosis and removal instructions.

### Test Connection

```shell
ssh -T git@github.com
```

Expected output:

```shell
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Use Case: Remote Servers

The same SSH key can authenticate to Linux servers, cloud VMs, and any SSH-enabled host.

### Add Key to Host

**Automatic** (recommended):

```shell
ssh-copy-id user@remote-host
```

This copies your public key to the remote host's `~/.ssh/authorized_keys`.

**Manual** (if `ssh-copy-id` unavailable):

```shell
cat ~/.ssh/id_ed25519.pub | ssh user@remote-host "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

### Connect

```shell
ssh user@remote-host
```

With a custom port:

```shell
ssh -p 2222 user@remote-host
```

### File Transfer (SCP)

**Upload** file to remote:

```shell
scp local-file.txt user@remote-host:~/
```

**Download** file from remote:

```shell
scp user@remote-host:~/remote-file.txt ./
```

**Upload directory** (recursive):

```shell
scp -r local-dir/ user@remote-host:~/
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Troubleshooting

### Permission Denied

**Symptom**:

```shell
Permission denied (publickey).
```

**Causes and fixes**:

1. **Key not added to target**:
   - For Git: Check key is in GitHub/GitLab SSH settings
   - For servers: Check `~/.ssh/authorized_keys` on remote host

2. **Key not in ssh-agent**:

   ```shell
   ssh-add -l                        # List loaded keys
   ssh-add ~/.ssh/id_ed25519         # Add if missing
   ```

3. **Wrong key being used**: Create `~/.ssh/config` to specify key per host:

   ```text
   Host github.com
     IdentityFile ~/.ssh/id_ed25519
   
   Host work-server
     HostName 192.168.1.100
     User admin
     IdentityFile ~/.ssh/id_work
   ```

### Agent Issues

**Symptom**: Key not persisting across terminal sessions.

**Fix**:

```shell
# Restart agent and re-add key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# macOS: use keychain for persistence
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

**Auto-start on shell login**: Add to `~/.bashrc` or `~/.zshrc`:

```shell
if [ -z "$SSH_AUTH_SOCK" ]; then
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_ed25519
fi
```

### Managing Known Hosts

The `~/.ssh/known_hosts` file stores fingerprints of SSH servers you have connected to. SSH checks this file to detect man-in-the-middle attacks.

**When to remove a host key**:

- The remote server was rebuilt or its SSH key was rotated (you see a `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED` error).
- A host key was added unintentionally, for example due to [Git URL rewriting](./use-cases-git.md#url-rewriting-issues) triggering an unexpected SSH connection.

**Remove a host key**:

```shell
ssh-keygen -R github.com
```

Replace `github.com` with the hostname you want to remove. The original `known_hosts` file is backed up automatically as `known_hosts.old`.

**View current known hosts**:

```shell
cat ~/.ssh/known_hosts
```

> [↑ Back to Table of Contents](#table-of-contents)

---

> Use Cases - SSH Authentication v1.1.0 - KemingHe/common-devx
