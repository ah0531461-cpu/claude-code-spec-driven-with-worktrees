# Implement Feature from Specification and Tasks

Execute implementation tasks one by one, tracking progress with TodoWrite.

## Usage

```
/spec-implement <spec-id>
```

**Required**: Spec ID (e.g., `2025-10-20-235900-add-jwt-authentication`)

## Instructions

### Step 1: Load Specification and Tasks

1. Read `.claude/specs/{spec-id}/spec.md`
   - If not found: Error "Spec not found"
2. Read `.claude/specs/{spec-id}/tasks.md`
   - If not found: Error "Tasks not found. Run /spec-plan {spec-id} first"
3. Parse all unchecked tasks: `- [ ] Task description - file: path`

### Step 2: Initialize TodoWrite

Create TodoWrite list with all tasks from tasks.md:
- Extract task description
- Extract file path
- Set status based on checkbox (completed vs pending)
- Mark first unchecked task as "in_progress"

### Step 3: Execute Tasks

For each unchecked task in order:

1. **Update TodoWrite**: Mark current task as "in_progress"

2. **Implement the task**:
   - Read relevant files
   - Make necessary changes
   - Follow spec requirements
   - Write/edit files as needed

3. **Update tasks.md**: Change `- [ ]` to `- [x]` for completed task

4. **Update TodoWrite**: Mark task as "completed"

5. **Move to next task**

### Step 4: Track Progress

Throughout implementation:
- Use TodoWrite to show current progress
- Update tasks.md checkboxes after each task
- Show user which task is being worked on
- Display completion percentage

### Step 5: Completion

When all tasks complete:

```
✓ Implementation complete!

Spec ID: {spec-id}
Tasks completed: {count}/{total}
Files modified: {file-list}

All tasks in .claude/specs/{spec-id}/tasks.md are now checked off.
```

## Important Rules

- MUST use TodoWrite to track progress
- MUST update tasks.md checkboxes as you go
- MUST complete tasks in order (respect dependencies)
- MUST mark task "in_progress" before starting work
- MUST mark task "completed" before moving to next
- ONE task in_progress at a time
- Show progress to user frequently

## Example Flow

```
/spec-implement 2025-10-20-235900-add-jwt-authentication

Loading spec and tasks...
Found 8 unchecked tasks

[TodoWrite: 8 tasks loaded]

Starting implementation...

Task 1/8: Install JWT library
[in_progress]
Running: composer require tymon/jwt-auth
✓ Complete

Task 2/8: Publish JWT config
[in_progress]
Running: php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\JWTAuthServiceProvider"
✓ Complete

... continues for all tasks ...

✓ Implementation complete!
  8/8 tasks completed
  Files modified: composer.json, config/jwt.php, app/Http/Middleware/JwtAuth.php, ...
```

## Progress Tracking

Example TodoWrite state during implementation:

```
[x] Install JWT library - file: composer.json
[x] Publish JWT config - file: config/jwt.php
[~] Generate JWT secret - file: .env      <- in_progress
[ ] Create auth middleware - file: app/Http/Middleware/JwtAuth.php
[ ] Add login endpoint - file: app/Http/Controllers/AuthController.php
[ ] Test login flow - file: tests/Feature/AuthTest.php
```
