# Guide - Common Shell Operations

> **Last Updated**: 2025-10-19 by Keming He

Essential shell commands and workflows organized by common developer scenarios for efficient command-line operations.

> [!NOTE]
>
> - **Related guides**: [Git operations](./guide-git-ops.md) for repository management
> - **AI prompts**: Commands in [prompt files](../prompts/) use piping techniques from this guide
> - **Platform**: Commands work on Linux, macOS, and Unix-like systems

## Table of Contents

- [Guide - Common Shell Operations](#guide---common-shell-operations)
  - [Table of Contents](#table-of-contents)
  - [Searching Files and Content](#searching-files-and-content)
    - [Finding Files](#finding-files)
    - [Searching Content](#searching-content)
  - [Output Control](#output-control)
    - [Piping to Cat](#piping-to-cat)
    - [Redirecting Output](#redirecting-output)
  - [File Operations](#file-operations)
    - [Viewing Files](#viewing-files)
    - [Navigation](#navigation)

## Searching Files and Content

Locate files and search through content efficiently across directories.

### Finding Files

```bash
# Find files by name
find . -name "*.md"                    # all markdown files in current directory
find /path/to/dir -name "README*"      # files starting with README
find . -iname "readme*"                # case-insensitive search

# Find by type
find . -type f -name "*.js"            # files only
find . -type d -name "node_modules"    # directories only

# Find by modification time
find . -type f -mtime -7               # modified in last 7 days
find . -type f -mtime +30              # modified more than 30 days ago

# Combine with actions
find . -name "*.log" -exec rm {} \;    # find and delete
find . -type f -name "*.md" | wc -l    # count files
```

### Searching Content

```bash
# Search in files
grep "pattern" file.txt                # search in single file
grep -r "pattern" .                    # recursive search in directory
grep -i "pattern" file.txt             # case-insensitive search

# Useful grep options
grep -n "pattern" file.txt             # show line numbers
grep -v "pattern" file.txt             # invert match (exclude pattern)
grep -l "pattern" *.txt                # list files with matches
grep -c "pattern" file.txt             # count matches

# Combine find and grep
find . -name "*.js" -exec grep -l "TODO" {} \;
find . -name "*.py" -exec grep -n "pattern" {} +    # search only Python files (portable)
```

> [⬆ Back to Table of Contents](#table-of-contents)

## Output Control

Manage command output for non-interactive execution and clean workflows.

### Piping to Cat

Use `| cat` to prevent interactive/pager mode and ensure complete output.

```bash
# Prevent pagers in git commands
git diff | cat                         # avoid interactive diff view
git log | cat                          # disable pager for log
git branch -a | cat                    # plain branch list

# Why pipe to cat?
# - AI agents and scripts need complete non-interactive output
# - Prevents commands from waiting for user input
# - Ensures all output is captured at once
# - Avoids terminal pager issues in automation

# Other non-interactive patterns
git status | cat                       # full status without interaction
man command | col -b                   # view entire manual at once (clean output)
```

### Redirecting Output

```bash
# Redirect to null (discard output)
command > /dev/null                    # discard standard output
command 2> /dev/null                   # discard error output
command > /dev/null 2>&1               # discard all output

# Redirect to files
command > output.txt                   # overwrite file with output
command >> output.txt                  # append output to file
command 2>&1 | tee output.txt          # save and display output

# Common use cases
npm install > /dev/null 2>&1           # silent installation
find . -name "*.tmp" 2> /dev/null      # ignore permission errors
```

> [⬆ Back to Table of Contents](#table-of-contents)

## File Operations

Common commands for viewing, navigating, and managing files.

### Viewing Files

```bash
# Display file contents
cat file.txt                           # view entire file
cat file1.txt file2.txt                # concatenate multiple files
head -n 20 file.txt                    # first 20 lines
tail -n 20 file.txt                    # last 20 lines
tail -f log.txt                        # follow file updates (logs)

# Paginated viewing
less file.txt                          # scrollable view (q to quit)
more file.txt                          # simple pager

# File information
wc -l file.txt                         # count lines
wc -w file.txt                         # count words
file document.pdf                      # identify file type
```

### Navigation

```bash
# Directory navigation
pwd                                    # print current directory
cd /path/to/directory                  # change directory
cd ..                                  # up one level
cd -                                   # previous directory
cd ~                                   # home directory

# List directory contents
ls                                     # basic list
ls -la                                 # detailed list with hidden files
ls -lh                                 # human-readable file sizes
ls -lt                                 # sort by modification time
tree                                   # hierarchical tree view (if installed)

# Create and remove
mkdir directory-name                   # create directory
mkdir -p path/to/nested/dir            # create nested directories
rmdir empty-directory                  # remove empty directory
rm -r directory                        # remove directory and contents
```

> [⬆ Back to Table of Contents](#table-of-contents)

---

> Common Shell Operations Guide v1.0.0 - KemingHe/common-devx
