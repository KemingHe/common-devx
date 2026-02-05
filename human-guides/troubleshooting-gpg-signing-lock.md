# Troubleshooting - GPG Signing Lock

> **Last Updated**: 2026-02-05 by Keming He

Git commit fails with GPG signing error due to lock files.

## Symptom

```shell
error: gpg failed to sign the data
fatal: failed to write commit object
```

## Diagnosis

```shell
gpg --list-secret-keys --keyid-format LONG
```

If you see `waiting for lock (held by XXXXX)`, you have a lock issue.

## Solution

### 1. Kill GPG Agent

```shell
gpgconf --kill gpg-agent
```

### 2. Remove Lock Files

```shell
find ~/.gnupg -name "*.lock" -delete
```

### 3. Verify Fix

```shell
gpg --list-secret-keys --keyid-format LONG    # Should respond immediately
echo "test" | gpg --clearsign                 # Should sign successfully
```

### 4. Retry Commit

Your git commit should now work.

## Alternative

Skip signing for one commit (temporary workaround):

```shell
git commit --no-gpg-sign -m "your message"
```

## Prevention

Lock files occur when GPG processes are interrupted. Run `gpgconf --kill gpg-agent` periodically to prevent stale processes.

---

> Troubleshooting - GPG Signing Lock v2.0.0 - KemingHe/common-devx
