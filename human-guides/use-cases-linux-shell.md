# Use Cases - Linux Shell

> **Last Updated**: 2026-02-05 by Keming He

Essential shell commands for developer workflows. Platform: Linux, macOS, Unix-like systems.

## Table of Contents

- [Use Cases - Linux Shell](#use-cases---linux-shell)
  - [Table of Contents](#table-of-contents)
  - [Search Files and Content](#search-files-and-content)
    - [Find Files](#find-files)
    - [Search Content](#search-content)
    - [Combined Search](#combined-search)
  - [View and Navigate Files](#view-and-navigate-files)
    - [View File Contents](#view-file-contents)
    - [File Info](#file-info)
    - [Navigate](#navigate)
    - [List Contents](#list-contents)
  - [Output Control](#output-control)
    - [Pipe to Cat](#pipe-to-cat)
    - [Redirect Output](#redirect-output)
  - [File Management](#file-management)
    - [Create](#create)
    - [Copy and Move](#copy-and-move)
    - [Delete](#delete)

## Search Files and Content

### Find Files

```shell
find . -name "*.md"               # Find by name (current dir)
find . -iname "readme*"           # Case-insensitive
find . -type f -name "*.js"       # Files only
find . -type d -name "src"        # Directories only
find . -mtime -7                  # Modified in last 7 days
```

### Search Content

```shell
grep "pattern" file.txt           # Search in file
grep -r "pattern" .               # Recursive search
grep -i "pattern" file.txt        # Case-insensitive
grep -n "pattern" file.txt        # Show line numbers
grep -l "pattern" *.md            # List matching files
```

### Combined Search

```shell
find . -name "*.js" -exec grep -l "TODO" {} \;    # Find files containing TODO
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## View and Navigate Files

### View File Contents

```shell
cat file.txt                      # Entire file
head -20 file.txt                 # First 20 lines
tail -20 file.txt                 # Last 20 lines
tail -f log.txt                   # Follow updates (logs)
less file.txt                     # Scrollable view (q to quit)
```

### File Info

```shell
wc -l file.txt                    # Count lines
file document.pdf                 # Identify file type
```

### Navigate

```shell
pwd                               # Current directory
cd /path/to/dir                   # Change directory
cd ..                             # Up one level
cd -                              # Previous directory
cd ~                              # Home directory
```

### List Contents

```shell
ls -la                            # Detailed with hidden files
ls -lh                            # Human-readable sizes
ls -lt                            # Sort by modification time
tree -L 2                         # Tree view, 2 levels (if installed)
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## Output Control

### Pipe to Cat

Prevents interactive/pager mode. Essential for scripts and AI agents.

```shell
git diff | cat                    # Avoid interactive diff
git log | cat                     # Disable pager
git status | cat                  # Full output, no interaction
```

### Redirect Output

```shell
command > file.txt                # Overwrite file
command >> file.txt               # Append to file
command > /dev/null               # Discard stdout
command 2> /dev/null              # Discard stderr
command > /dev/null 2>&1          # Discard all output
command 2>&1 | tee output.txt     # Save and display
```

> [↑ Back to Table of Contents](#table-of-contents)

---

## File Management

### Create

```shell
mkdir directory                   # Create directory
mkdir -p path/to/nested/dir       # Create nested directories
touch file.txt                    # Create empty file
```

### Copy and Move

```shell
cp source.txt dest.txt            # Copy file
cp -r source/ dest/               # Copy directory
mv old.txt new.txt                # Rename/move
```

### Delete

```shell
rm file.txt                       # Delete file
rm -r directory/                  # Delete directory
rmdir empty-dir/                  # Delete empty directory only
```

> [↑ Back to Table of Contents](#table-of-contents)

---

> Use Cases - Linux Shell v2.0.0 - KemingHe/common-devx
