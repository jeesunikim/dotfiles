# dotfiles

## Setup

Add `bin/` to your PATH in `.zshrc` (or `.bashrc`):

```bash
export PATH="$HOME/dotfiles/bin:$PATH"
```

## Scripts

### `worktree`

Creates a git worktree as a sibling directory, copies `node_modules` (using copy-on-write when possible), common config files, and drops you into the new directory.

```bash
. worktree <branch-name>
```

The leading `.` (source) is required so the `cd` at the end changes your shell's directory.

**Examples:**

```bash
. worktree issue-1991          # creates ../my-project-issue-1991
. worktree feature/auth        # creates ../my-project-feature_auth
. worktree -v issue-1991       # verbose output
```

**What it does:**

1. Creates a worktree (or `cd`s into it if it already exists)
2. Copies `node_modules` using CoW (near-instant, no extra disk space)
3. Copies `.env.local`, `.tool-versions`, `mise.toml` if present
4. Runs `.worktree-setup.sh` if the repo has one