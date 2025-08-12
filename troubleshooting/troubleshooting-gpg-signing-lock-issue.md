# Troubleshooting - GPG Signing Issue

> Update on 2025-08-11 by @KemingHe

## Problem

Git commit fails with:

```shell
error: gpg failed to sign the data
fatal: failed to write commit object
```

## Quick Diagnosis

```shell
# Check if GPG signing is enabled
git config --get commit.gpgsign

# Test GPG database access
gpg --list-secret-keys --keyid-format LONG
```

If you see `waiting for lock (held by XXXXX)` messages, you have a lock issue.

## Solution

### Step 1 - Kill GPG Agent

```bash
gpgconf --kill gpg-agent
```

### Step 2 - Find and Remove Lock Files

```bash
# Find lock files
find ~/.gnupg -name "*.lock" -ls

# Remove them (common locations)
rm ~/.gnupg/public-keys.d/pubring.db.lock
rm ~/.gnupg/*.lock
```

### Step 3 - Verify Fix

```bash
# Should list your keys without timeout
gpg --list-secret-keys --keyid-format LONG

# Test signing capability
echo "test" | gpg --clearsign
```

### Step 4 - Retry Git Commit

Your commit should now work with GPG signing.

## Alternative Solutions

- **Nuclear option**: Restart computer (always works)
- **Temporary workaround**: Disable signing for one commit:

  ```bash
  git commit --no-gpg-sign -m "your message"
  ```

## Prevention

Lock files usually occur when:

- GPG processes are forcefully terminated
- System crashes during GPG operations
- Multiple GPG operations run simultaneously

Regular `gpgconf --kill gpg-agent` can prevent buildup of stale processes.

---

> GPG Signing Issue Resolution - KemingHe/common-devx
