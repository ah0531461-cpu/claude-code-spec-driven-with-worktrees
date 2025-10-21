# Spec-Driven Development Setup Instructions for Claude Code

**Purpose**: These instructions guide Claude Code to automatically set up the spec-driven development workflow with git worktrees in your project.

## Prerequisites Check

Before starting, verify:
1. You are in the root directory of a git repository
2. Git version is 2.15.0 or higher (run: `git --version`)
3. You have write permissions in this directory

## Setup Steps

### Step 1: Create .claude Directory Structure

Create the following directory structure:

```
.claude/
├── commands/
├── scripts/
├── templates/
└── specs/
```

**Action**: Create these directories if they don't exist.

### Step 2: Download Command Files

Download the following slash command files to `.claude/commands/`:

1. **spec.md** - Generate feature specifications
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/commands/spec.md`
   - Save to: `.claude/commands/spec.md`

2. **spec-plan.md** - Create implementation task plans
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/commands/spec-plan.md`
   - Save to: `.claude/commands/spec-plan.md`

3. **spec-implement.md** - Execute implementation tasks
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/commands/spec-implement.md`
   - Save to: `.claude/commands/spec-implement.md`

**Action**: Use WebFetch or curl to download each file and save it to the correct location.

### Step 3: Download Script Files

Download the following shell scripts to `.claude/scripts/`:

1. **create-worktree.sh** - Create new feature worktree
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/scripts/create-worktree.sh`
   - Save to: `.claude/scripts/create-worktree.sh`

2. **merge-worktree.sh** - Merge and cleanup worktree
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/scripts/merge-worktree.sh`
   - Save to: `.claude/scripts/merge-worktree.sh`

3. **checkout-worktree.sh** - Switch to existing worktree
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/scripts/checkout-worktree.sh`
   - Save to: `.claude/scripts/checkout-worktree.sh`

4. **delete-worktree.sh** - Remove worktree without merging
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/scripts/delete-worktree.sh`
   - Save to: `.claude/scripts/delete-worktree.sh`

**Action**: Download each script and save to `.claude/scripts/`.

### Step 4: Download Template Files

Download the following template files to `.claude/templates/`:

1. **spec.template.md** - Specification template
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/templates/spec.template.md`
   - Save to: `.claude/templates/spec.template.md`

2. **tasks.template.md** - Task plan template
   - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/templates/tasks.template.md`
   - Save to: `.claude/templates/tasks.template.md`

**Action**: Download each template and save to `.claude/templates/`.

### Step 5: Download Governance Rules

Download the governance rules file:

- **rules.md** - Quality governance rules (customize this for your tech stack!)
  - URL: `https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/.claude/rules.md`
  - Save to: `.claude/rules.md`

**Action**: Download and save to `.claude/rules.md`.

### Step 6: Make Scripts Executable

Make all shell scripts executable:

```bash
chmod +x .claude/scripts/*.sh
```

**Action**: Run this command to make scripts executable.

### Step 7: Update .gitignore

Add the following line to `.gitignore` (create file if it doesn't exist):

```
# Specification files (used during development only, deleted with worktree)
.claude/specs/
```

**Action**:
- If `.gitignore` exists: Append the above lines
- If `.gitignore` doesn't exist: Create it with the above content
- If `.claude/specs/` is already in `.gitignore`: Skip this step

### Step 8: Verify Setup

Verify the installation by checking:

1. Directory structure exists:
   ```bash
   ls -la .claude/
   ```
   Should show: commands/, scripts/, templates/, specs/, rules.md

2. All command files exist:
   ```bash
   ls .claude/commands/
   ```
   Should show: spec.md, spec-plan.md, spec-implement.md

3. All script files exist and are executable:
   ```bash
   ls -la .claude/scripts/
   ```
   Should show: create-worktree.sh, merge-worktree.sh, checkout-worktree.sh, delete-worktree.sh (all with execute permissions)

4. All template files exist:
   ```bash
   ls .claude/templates/
   ```
   Should show: spec.template.md, tasks.template.md

5. Rules file exists:
   ```bash
   ls .claude/rules.md
   ```

**Action**: Run verification commands and report results.

## Post-Setup Instructions

After setup is complete, inform the user:

### ✅ Setup Complete!

Spec-driven development with git worktrees has been set up successfully!

### Next Steps

1. **Customize governance rules**: Edit `.claude/rules.md` to match your tech stack and coding standards

2. **Test the workflow**: Create your first feature
   ```bash
   ./.claude/scripts/create-worktree.sh "Test feature"
   ```

3. **Learn the commands**:
   - `/spec <description>` - Generate a specification (use in plan mode: Shift+Tab)
   - `/spec-plan <spec-id>` - Create task plan from spec
   - `/spec-implement <spec-id>` - Execute implementation tasks

4. **Read the documentation**: See the full README at: https://github.com/priyashpatil/claude-code-spec-driven-with-worktrees

### Important Reminders

- **This is a template**: Customize `.claude/rules.md` for your project's needs
- **Specs are temporary**: The `.claude/specs/` directory is gitignored and should be deleted when worktrees are merged
- **Use plan mode**: Always press `Shift+Tab` before running `/spec` command

### Quick Reference

**Worktree Scripts**:
- Create: `./.claude/scripts/create-worktree.sh "description"`
- Merge: `./.claude/scripts/merge-worktree.sh`
- Switch: `./.claude/scripts/checkout-worktree.sh`
- Delete: `./.claude/scripts/delete-worktree.sh`

**Slash Commands** (in Claude Code):
- `/spec` - Generate specification
- `/spec-plan <spec-id>` - Plan implementation
- `/spec-implement <spec-id>` - Execute tasks

---

## Troubleshooting

If setup fails:

1. **Permission errors**: Ensure you have write access to the current directory
2. **Git errors**: Verify you're in a git repository (`git status`)
3. **Network errors**: Check internet connection for downloading files
4. **File exists errors**: This is usually fine - files may already be set up

If you encounter issues, see: https://github.com/priyashpatil/claude-code-spec-driven-with-worktrees/issues

## Implementation Notes for Claude Code

When executing this setup:

1. **Use WebFetch** to download each file from the GitHub raw URLs
2. **Use Write tool** to save each file to the correct location
3. **Use Bash tool** to:
   - Create directories (`mkdir -p`)
   - Make scripts executable (`chmod +x`)
   - Verify installation (`ls` commands)
4. **Use Edit tool** to update .gitignore if it exists, or Write tool if it doesn't
5. **Report progress** to the user as each step completes
6. **Handle errors gracefully**: If a file already exists, inform the user and skip
7. **Verify at the end**: Run all verification commands and report any issues

Execute steps sequentially and inform the user of progress throughout.
