# Claude Code Spec-Driven Development with Git Worktrees

A structured workflow system for building high-quality software features using specification-driven development, automated task planning, and isolated git worktrees.

> **⚠️ IMPORTANT DISCLAIMER**
>
> This is **NOT** a complete, production-ready tool. This is a **simple implementation** and **template** of spec-driven development with personal preferences baked in. The whole point of this repository is to serve as a **starting point** that you can modify and customize based on your project's needs.
>
> **Key Customization Points**:
>
> - **`.claude/rules.md`**: This is YOUR governance file. Update it based on your tech stack, coding standards, and team preferences.
> - **Slash commands**: Modify the command prompts in `.claude/commands/` to match your workflow.
> - **Templates**: Adjust `.claude/templates/` to fit your documentation style.
> - **Scripts**: Enhance the shell scripts with your own logic (e.g., Jira integration, Slack notifications).
>
> **Fork this repo, customize it, and make it yours!**

## Overview

This project provides a comprehensive framework for developing software features with:

- **📋 Structured Specifications**: Generate detailed feature specs with functional requirements (FR-xxx), non-functional requirements (NFR-xxx), and acceptance criteria
- **🌳 Git Worktree Isolation**: Develop each feature in its own isolated worktree, keeping your main workspace clean
- **🤖 AI-Powered Workflow**: Use Claude Code slash commands to automate specification generation, task planning, and implementation
- **✅ Quality Governance**: Enforce mandatory testing, proper documentation, and consistent code quality through automated rules
- **🔄 Streamlined Workflow**: From idea to implementation with guided, trackable steps

### Why Use This Workflow?

#### The Context Loss Problem

While Claude Code's plan mode is useful, it has a critical limitation: **long discussions and back-and-forth interactions often cause Claude to lose the original context too early**. When you're planning a complex feature, the conversation can drift, and important details from the beginning get lost.

**Spec-driven development solves this by separating concerns**:

1. **Draft the spec** (one session) - All requirements and context captured in a document
2. **Plan the tasks** (separate session) - Read the spec, no context loss
3. **Implement** (another session) - Read spec + tasks, execute methodically

Each phase can happen in a **completely separate Claude session** without any context issues because everything is written down in structured documents.

#### Additional Benefits

**Traditional ad-hoc development problems**:

- Cluttering your main workspace with in-progress code
- Switching branches and losing context
- Forgetting to write tests
- Incomplete or inconsistent documentation
- Ad-hoc task management leading to forgotten requirements

**This workflow provides**:

- **Context Preservation**: Specs, plans, and progress are stored as documents, readable across sessions
- **Worktree Isolation**: Each feature lives in its own directory (separate worktree, same repo)
- **Mandatory Quality**: Tests are required, not optional (enforced by governance rules)
- **Structured Progress**: Track implementation with checkboxes and todo lists
- **Customizable Governance**: Define your own rules in `.claude/rules.md` based on your tech stack
- **No Context Drift**: Claude can always re-read the spec to understand what needs to be built

## Getting Started

### Quick Start (1 Minute Setup)

Want to get started right away? Open Claude Code in your project and say:

```
Please read and follow the instructions in this file to set up spec-driven development in my project: https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/setup-sdd.md
```

Claude will automatically download and configure everything. Skip to [Post-Installation](#post-installation-customize-for-your-project) when done.

---

### Prerequisites

- **Claude Code CLI** (v1.0.0 or later): [Installation guide](https://docs.claude.com/en/docs/claude-code)
- **Git** (v2.15.0+ for worktree support)
- A git repository where you want to use this workflow

### Installation

The easiest way to set up this workflow in your project:

1. **Navigate to your project directory**:

   ```bash
   cd /path/to/your/project
   ```

2. **Open Claude Code**:

   ```bash
   claude
   ```

3. **Run the setup command**:
   ```
   Please read and follow the instructions in this file to set up spec-driven development in my project: https://raw.githubusercontent.com/priyashpatil/claude-code-spec-driven-with-worktrees/main/setup-sdd.md
   ```

Claude will automatically:

- Download all necessary files (commands, scripts, templates, rules)
- Create the `.claude/` directory structure
- Make scripts executable
- Update your `.gitignore`
- Verify the installation

**That's it!** The workflow is ready to use.

### Directory Structure

```
your-project/
├── .claude/
│   ├── commands/              # Slash commands for Claude Code
│   │   ├── spec.md           # /spec - Generate specification
│   │   ├── spec-plan.md      # /spec-plan - Create task plan
│   │   └── spec-implement.md # /spec-implement - Execute tasks
│   ├── scripts/              # Automation scripts
│   │   ├── create-worktree.sh    # Create new feature worktree
│   │   ├── merge-worktree.sh     # Merge and cleanup worktree
│   │   ├── checkout-worktree.sh  # Switch to existing worktree
│   │   └── delete-worktree.sh    # Remove worktree without merging
│   ├── templates/            # Spec and task templates
│   │   ├── spec.template.md
│   │   └── tasks.template.md
│   ├── specs/                # Generated specs (gitignored - ephemeral, not committed)
│   └── rules.md              # Quality governance rules (customize for your stack)
├── .gitignore                # Includes .claude/specs/
└── your-project-files...
```

> **Note**: The `specs/` directory is intentionally gitignored. Specs are temporary development aids that get deleted when worktrees are merged or removed.

### Post-Installation: Customize for Your Project

**IMPORTANT**: After installation, customize the workflow for your project:

1. **Edit `.claude/rules.md`**:

   - Update rules to match your tech stack (Python, JavaScript, Go, etc.)
   - Add your coding standards and conventions
   - Specify your testing framework requirements
   - Define project-specific quality gates

2. **Optional: Modify templates**:

   - Customize `.claude/templates/spec.template.md` for your spec format
   - Adjust `.claude/templates/tasks.template.md` for your task structure

3. **Test the setup**:

   ```bash
   # Create a test worktree
   ./.claude/scripts/create-worktree.sh "Test setup"
   ```

   Then in the Claude Code session that opens:

   > **🔑 Press `Shift+Tab` to enter plan mode first!**

   ```
   /spec Add a simple hello world endpoint
   ```

4. **Understanding spec files**:

   > ⚠️ **Important**: `.claude/specs/` is **gitignored**. Spec files are development aids only - NOT documentation to be committed. Your **tests are the real specs**. Once implementation is complete with proper test coverage, spec files can be deleted. This is intentional design, not an oversight.

**Remember**: This is a template, not a one-size-fits-all solution. Make it yours!

## Core Concepts

### Specification-Driven Development

Every feature starts with a specification that includes:

1. **Functional Requirements (FR-xxx)**: What the system must do

   - Example: `FR-001: System MUST authenticate users via JWT tokens`

2. **Non-Functional Requirements (NFR-xxx)**: How the system should behave

   - Example: `NFR-001: System SHOULD respond to auth requests within 200ms`

3. **Acceptance Criteria**: Given/When/Then scenarios

   - Example: `Given a valid JWT token, When the user accesses a protected route, Then the request succeeds`

4. **Technical Notes**: Implementation details, tech stack, architecture decisions

5. **Out of Scope**: Clear boundaries of what's NOT included

### Git Worktrees

Git worktrees let you check out multiple branches simultaneously in different directories:

```
my-project/                    # Main workspace (main branch)
my-project-worktrees/
  ├── add-jwt-authentication/  # Feature worktree #1
  ├── implement-user-profile/  # Feature worktree #2
  └── fix-login-bug/           # Feature worktree #3
```

**Benefits**:

- Work on multiple features without branch switching
- Keep main workspace clean and stable
- Test features independently
- No WIP commits polluting your main branch

### Three-Phase Workflow

1. **`/spec <description>`**: Generate a specification through interactive Q&A
2. **`/spec-plan <spec-id>`**: Break down the spec into actionable tasks
3. **`/spec-implement <spec-id>`**: Execute tasks one by one with progress tracking

## Complete Workflow Example

> **⚠️ About Spec Files**: The `.claude/specs/` directory is **gitignored by design**. Specs are meant as development aids only - your **unit tests and feature tests** are the real specifications. Once implementation is complete and tests are written, spec files can be deleted. They're ephemeral, not part of your codebase.

**Important**: ALL commands run from your **project root** directory. The workflow automatically handles moving between project root and worktree.

### Step 1: Create Worktree (from project root)

```bash
# Terminal: In your project root directory
./.claude/scripts/create-worktree.sh "Add JWT authentication"
```

**What happens**:
- Script generates branch name: `add-jwt-authentication`
- Creates worktree in: `../your-project-worktrees/add-jwt-authentication/`
- **Automatically starts Claude Code in the worktree directory**
- You're now in Claude Code, ready to work

---

### Step 2-4: Development (in Claude Code session)

**You're now in the worktree's Claude Code session. Run these commands here:**

> **🔑 IMPORTANT: Press `Shift+Tab` first to enter plan mode before running `/spec`!**

#### Generate Specification

```
/spec Add JWT authentication with login, token refresh, and protected routes
```

Claude will ask clarifying questions, then generate a spec in `.claude/specs/{spec-id}/spec.md`.

#### Create Task Plan

```
/spec-plan {spec-id}
```

Claude generates a task breakdown in `.claude/specs/{spec-id}/tasks.md`.

#### Implement

```
/spec-implement {spec-id}
```

Claude executes all tasks, tracking progress with todo lists.

---

### Step 5: Commit and Exit (in Claude Code session)

When implementation is complete:

```
# Ask Claude to commit your changes
Please commit these changes with an appropriate commit message
```

Claude will create a commit for you. Then:

```
# Exit Claude Code (press Ctrl+D or type /exit)
```

**What happens**: You're automatically returned to your **project root directory**.

---

### Step 6: Merge or Create PR (from project root)

> **Note**: The merge-worktree script is **OPTIONAL** and primarily for personal projects or demos. For team projects, you'd typically create a Pull Request on GitHub instead.

**Option A: Direct Merge (personal projects)**

```bash
# Terminal: You're back in project root now
./.claude/scripts/merge-worktree.sh
```

Select your worktree from the interactive menu. The script merges to main and cleans up the worktree.

**Option B: Create Pull Request (recommended for teams)**

```bash
# Push your branch (from project root)
git push -u origin add-jwt-authentication

# Create PR using GitHub CLI
gh pr create --title "Add JWT authentication" --body "Implements JWT auth with login, refresh, and protected routes"
```

After PR is merged on GitHub, clean up the worktree:

```bash
./.claude/scripts/delete-worktree.sh
```

---

### Summary: Where Commands Run

| Step | Location | Command |
|------|----------|---------|
| 1. Create worktree | **Project root** (terminal) | `./claude/scripts/create-worktree.sh` |
| 2-4. Development | **Worktree** (Claude Code session) | `/spec`, `/spec-plan`, `/spec-implement` |
| 5. Commit & exit | **Worktree** (Claude Code session) | Ask Claude to commit, then exit |
| 6. Merge/PR | **Project root** (terminal) | `merge-worktree.sh` or `gh pr create` |

**Key Point**: You start in project root, the script takes you to the worktree, and exiting Claude brings you back to project root automatically.

## Command Reference

### Slash Commands (Use in Claude Code)

#### `/spec <description>`

Generate a feature specification through interactive planning.

> **⚠️ REQUIRED: Press `Shift+Tab` to enter plan mode BEFORE running this command!**

**Usage**:

```
# Step 1: Press Shift+Tab to enter plan mode
# Step 2: Run the command below
/spec Add user profile page with avatar upload
```

**Process**:

1. Reads governance rules from `.claude/rules.md`
2. Asks clarifying questions about your feature
3. Presents a plan for the spec
4. Waits for your approval
5. Generates and saves spec to `.claude/specs/{spec-id}/spec.md`

**Output**: Spec ID that you'll use in next commands

---

#### `/spec-plan <spec-id>`

Create detailed implementation tasks from a specification.

**Usage**:

```
/spec-plan 2025-10-21-143022-add-jwt-authentication
```

**Process**:

1. Reads the specification
2. Reads quality governance rules
3. Breaks down spec into specific tasks with file paths
4. Organizes tasks into phases (Setup, Implementation, Testing)
5. Validates against rules (mandatory tests, file paths, etc.)
6. Saves to `.claude/specs/{spec-id}/tasks.md`

**Output**: Tasks file with checkboxes ready for implementation

---

#### `/spec-implement <spec-id>`

Execute implementation tasks with progress tracking.

**Usage**:

```
/spec-implement 2025-10-21-143022-add-jwt-authentication
```

**Process**:

1. Loads spec and tasks
2. Creates TodoWrite list for progress tracking
3. Executes each unchecked task sequentially:
   - Marks as "in_progress"
   - Makes code changes
   - Updates `tasks.md` checkbox
   - Marks as "completed"
4. Reports completion with modified files

**Output**: Implemented feature with all tasks checked off

---

### Worktree Scripts (Use in Terminal)

#### `create-worktree.sh`

Create a new git worktree for feature development.

**Usage**:

```bash
./.claude/scripts/create-worktree.sh "Add user profile page"
```

**What it does**:

1. Uses Claude to generate a branch name from your description
2. Creates worktree at `../project-worktrees/branch-name/`
3. Creates and checks out the new branch
4. Automatically starts Claude Code in the worktree

---

#### `merge-worktree.sh`

Merge a worktree branch into main and clean up.

**Usage**:

```bash
# Option 1: From within worktree (auto-detects)
./.claude/scripts/merge-worktree.sh

# Option 2: From main repo (interactive selection)
cd /path/to/main/repo
./.claude/scripts/merge-worktree.sh
```

**What it does**:

1. Checks for uncommitted changes (fails if found)
2. Switches to main branch
3. Merges your feature branch (fails gracefully on conflicts)
4. Removes the worktree directory
5. Deletes the feature branch
6. Shows confirmation and recent commits

**Conflict handling**: If merge conflicts occur, the script aborts and provides instructions for manual resolution.

---

#### `checkout-worktree.sh`

Switch to an existing worktree.

**Usage**:

```bash
./.claude/scripts/checkout-worktree.sh
# Shows interactive list of available worktrees
```

**What it does**:

1. Lists all existing worktrees
2. Prompts you to select one
3. Changes directory to the selected worktree
4. Optionally starts Claude Code

---

#### `delete-worktree.sh`

Remove a worktree without merging (for abandoned features).

**Usage**:

```bash
./.claude/scripts/delete-worktree.sh
# Shows interactive list with confirmation
```

**What it does**:

1. Lists all worktrees
2. Prompts for selection
3. Asks for confirmation
4. Removes worktree directory
5. Deletes the branch

**Use when**: You want to discard a feature without merging it.

## Quality Governance Rules

The `.claude/rules.md` file enforces quality standards automatically.

> **📝 Customization Note**: The rules below are **example rules** based on personal preferences. You should **modify `.claude/rules.md`** to match your:
>
> - Tech stack (e.g., different testing frameworks, language-specific conventions)
> - Team standards (e.g., code review requirements, documentation style)
> - Project requirements (e.g., security policies, performance benchmarks)
>
> **This is YOUR governance file - make it work for YOUR project!**

### Critical Rules (MUST Enforce)

#### Tests are Mandatory

- **Tests are REQUIRED for all features** - NO EXCEPTIONS
- NEVER mark tests as "optional" or "if time permits"
- Every spec MUST include test requirements
- Every task plan MUST include test tasks in Testing phase

#### Requirements Format

- Functional requirements: `FR-001`, `FR-002`, etc.
- Non-functional requirements: `NFR-001`, `NFR-002`, etc.
- Minimum 3 functional requirements per spec
- Each requirement must start with "System MUST" or "System SHOULD"

#### Task Format

- NO tasks marked as "optional" or "nice-to-have"
- Every task MUST include: `- [ ] Description - file: path/to/file.ext`
- Tasks MUST be verb-based: "Create", "Add", "Implement", "Update", "Test"
- NO vague tasks like "Add functionality"
- Minimum 3 tasks per implementation plan

### Quality Rules (SHOULD Enforce)

#### Specification Structure

- Include "Out of Scope" section to clarify boundaries
- Acceptance criteria SHOULD use Given/When/Then format
- Technical notes MUST specify technology choices
- Overview must explain what, why, and how

#### Task Organization

- **Phase 1: Setup** - Dependencies, configuration, scaffolding
- **Phase 2: Implementation** - Core feature code
- **Phase 3: Testing** - Test creation and validation
- Testing phase MUST come after Implementation
- Each phase should have 2-5 tasks

### Validation Checkpoints

Claude automatically validates:

**During `/spec` generation**:

- [ ] Tests are not marked optional
- [ ] At least 3 FR requirements with proper IDs
- [ ] At least 1 NFR requirement
- [ ] Acceptance criteria present
- [ ] Out of Scope section exists

**During `/spec-plan` generation**:

- [ ] No tasks marked as optional
- [ ] All tasks have file paths
- [ ] Testing phase exists and has tasks
- [ ] All tasks are verb-based
- [ ] Minimum 3 tasks total

**If validation fails**: Claude shows a clear error and regenerates the spec/tasks.

## Best Practices

### When to Create Worktrees

**Good use cases**:

- New features that take multiple sessions
- Bug fixes that require experimentation
- Refactoring efforts
- Working on multiple features in parallel

**Not necessary for**:

- Quick typo fixes
- One-line changes
- Documentation updates
- Very simple bug fixes

### Spec Writing Tips

1. **Be specific in your description**:

   - ❌ "Add authentication"
   - ✅ "Add JWT authentication with login, logout, token refresh, and protected routes using tymon/jwt-auth"

2. **Answer clarifying questions thoughtfully**: Claude's questions help create better specs

3. **Review the spec before implementing**: The spec is your contract - make sure it's complete

4. **Update the spec if requirements change**: Keep it as a living document during development

5. **Don't commit spec files**: Remember, `.claude/specs/` is gitignored. Your tests are the real documentation.

### Managing Multiple Features

You can work on multiple features simultaneously:

```bash
# All from project root - open multiple terminals
# Terminal 1: Feature 1
./.claude/scripts/create-worktree.sh "Add JWT authentication"
# (Claude starts in worktree, do your work, commit, exit)

# Terminal 2: Feature 2
./.claude/scripts/create-worktree.sh "Add user profile page"
# (Claude starts in worktree, do your work, commit, exit)

# Terminal 3: Feature 3
./.claude/scripts/create-worktree.sh "Add email notifications"
# (Claude starts in worktree, do your work, commit, exit)
```

Each feature is isolated in its own worktree directory.

### Integration Strategy

> **Personal Preference Note**: The approach below reflects the author's workflow for personal projects. Adapt to your team's needs.

**For Team Projects (Recommended)**:

```bash
# From project root (after exiting Claude)
git push -u origin feature-branch-name
gh pr create --title "Feature title" --body "Description"

# After PR is merged, clean up
./.claude/scripts/delete-worktree.sh
```

**For Personal Projects (Optional)**:

The `merge-worktree.sh` script is provided for quick iteration on personal projects:

```bash
# From project root (where you land after exiting Claude)
./.claude/scripts/merge-worktree.sh
```

This directly merges to main and cleans up the worktree. **Use this only if you're working alone and comfortable with direct main branch commits.**

### Commit Practices

**During Development**:

- Commit frequently in the worktree (it's isolated, safe to experiment)
- Use Claude to help create good commit messages: "Please commit these changes with an appropriate message"
- Squash commits before merging if you made many WIP commits

**Remember**: All commits happen in the worktree (via Claude or manual git commands). After exiting Claude, you're back in project root ready to push or merge.

## Troubleshooting

### Common Issues

#### "Branch already exists" error

**Problem**: You're trying to create a worktree for a branch that already exists.

**Solution**:

```bash
# Check existing worktrees
git worktree list

# Option 1: Use checkout-worktree.sh to switch to existing worktree
./.claude/scripts/checkout-worktree.sh

# Option 2: Delete the old worktree first
./.claude/scripts/delete-worktree.sh
```

---

#### "Spec not found" error

**Problem**: Running `/spec-plan` or `/spec-implement` with wrong spec ID.

**Solution**:

```bash
# List all specs
ls .claude/specs/

# Use the full spec ID (format: YYYY-MM-DD-HHMMSS-slug)
/spec-plan 2025-10-21-143022-add-jwt-authentication
```

---

#### Merge conflicts

**Problem**: `merge-worktree.sh` fails with conflicts.

**Solution**:

```bash
# The script automatically aborts the merge
# Follow the instructions it provides:

# 1. Stay in main worktree
cd /path/to/main/project

# 2. Manually merge
git merge branch-name

# 3. Resolve conflicts in your editor
# Edit conflicting files, then:
git add .
git commit -m "Merge branch-name"

# 4. Clean up worktree
./.claude/scripts/merge-worktree.sh
# Now it will only clean up (merge is already done)
```

---

#### Worktree has uncommitted changes

**Problem**: `merge-worktree.sh` fails because of uncommitted changes.

**Solution**:

```bash
# Option 1: Commit the changes
cd /path/to/worktree
git add .
git commit -m "Complete feature implementation"

# Option 2: Stash the changes
git stash
# Then merge, then apply stash in main if needed

# Option 3: Discard the changes
git reset --hard HEAD
```

---

#### Validation errors during spec generation

**Problem**: Claude reports "Rule Violation: Tests marked as optional".

**Solution**: This is by design. Claude will automatically regenerate the spec without marking tests as optional. If it persists, check `.claude/rules.md` to understand the requirements.

---

#### Can't find worktree scripts

**Problem**: `bash: ./.claude/scripts/create-worktree.sh: No such file or directory`

**Solutions**:

1. Make sure you're in the project root directory
2. Check if scripts exist: `ls .claude/scripts/`
3. Make them executable: `chmod +x .claude/scripts/*.sh`

---

#### Claude Code doesn't recognize slash commands

**Problem**: `/spec` doesn't trigger the command.

**Solutions**:

1. Make sure you're running Claude Code CLI, not the web interface
2. Verify `.claude/commands/` directory exists
3. Check command files exist:
   ```bash
   ls .claude/commands/
   # Should show: spec.md, spec-plan.md, spec-implement.md
   ```
4. Restart Claude Code

### Cleaning Up Orphaned Worktrees

If worktree directories were deleted manually (not recommended), clean up git's records:

```bash
# List all worktrees (including broken ones)
git worktree list

# Prune deleted worktrees
git worktree prune

# Remove specific worktree entry
git worktree remove /path/to/worktree
```

### Resetting Everything

To start fresh:

```bash
# 1. Remove all worktrees
./.claude/scripts/delete-worktree.sh
# (run for each worktree)

# 2. Clean up git records
git worktree prune

# 3. Remove all specs
rm -rf .claude/specs/*

# 4. Verify clean state
git worktree list  # Should show only main repo
git status         # Should be clean
```

## Advanced Usage

### Customizing Quality Rules for Your Tech Stack

**IMPORTANT**: The rules in `.claude/rules.md` are examples. You **MUST** customize them for your project.

#### Example: Python/Django Project

```markdown
### Python/Django Specific Rules

- All models MUST include `__str__` method
- All views MUST use class-based views (no function views)
- All database queries MUST use Django ORM (no raw SQL without justification)
- All API endpoints MUST use Django REST Framework serializers
- Tests MUST use pytest, not unittest
- Code coverage MUST be above 80%
```

#### Example: React/TypeScript Project

```markdown
### React/TypeScript Specific Rules

- All components MUST be functional (no class components)
- All props MUST have TypeScript interfaces
- All API calls MUST use React Query
- All forms MUST use react-hook-form with Zod validation
- Tests MUST use React Testing Library (no Enzyme)
- All components MUST be in separate files from their tests
```

#### Example: Backend API Project

```markdown
### API Specific Rules

- All endpoints MUST have rate limiting
- All database queries MUST use parameterized statements
- All API responses MUST follow JSON:API specification
- All endpoints MUST have OpenAPI/Swagger documentation
- All authentication MUST use JWT tokens
- All passwords MUST be hashed with bcrypt
```

Claude will enforce these rules during spec and task generation. **Customize them to match your project's needs!**

### Custom Task Templates

Modify `.claude/templates/tasks.template.md` to change task structure:

```markdown
## Phase 1: Setup

- [ ] {{TASK}} - file: {{FILE}} - estimate: {{HOURS}}h

## Phase 2: Implementation

...
```

### Working with Remote Teams

```bash
# Share specs via PR description
git checkout -b feature-branch
# ... develop feature ...
git commit -m "Add feature X"

# Include spec in PR description:
gh pr create --body "$(cat .claude/specs/2025-10-21-143022-feature-x/spec.md)"
```

## Contributing

This is a **template repository** meant to be forked and customized for your own needs. However, if you have improvements to the base template that would benefit others:

1. Fork the repository
2. Create a worktree for your improvement: `./.claude/scripts/create-worktree.sh "Improve X"`
3. Make your changes
4. Test thoroughly
5. Submit a pull request

**Sharing Your Customizations**: If you've created an interesting customization (e.g., specific tech stack rules, integration with tools like Jira), consider sharing it in [GitHub Discussions](https://github.com/priyashpatil/claude-code-spec-driven-with-worktrees/discussions) so others can learn from your approach!

## License

MIT License

Copyright (c) 2025 Priyash Patil

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

See the [LICENSE](LICENSE) file for full details.

## Support

- **Issues**: [GitHub Issues](https://github.com/priyashpatil/claude-code-spec-driven-with-worktrees/issues)
- **Discussions**: [GitHub Discussions](https://github.com/priyashpatil/claude-code-spec-driven-with-worktrees/discussions)
- **Claude Code Docs**: [docs.claude.com](https://docs.claude.com/en/docs/claude-code)

## Credits

Created by [Priyash Patil](https://github.com/priyashpatil)

Built with [Claude Code](https://claude.ai/code) by Anthropic

---

**Happy coding with structured, quality-driven development!** 🚀
