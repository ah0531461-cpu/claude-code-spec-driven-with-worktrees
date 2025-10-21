# Create Implementation Tasks from Specification

Generate a detailed task breakdown for implementing a feature specification.

## Usage

```
/spec-plan <spec-id>
```

**Required**: Spec ID (e.g., `2025-10-20-235900-add-jwt-authentication`)

## Instructions

### Step 1: Read Governance Rules

**FIRST**: Read `.claude/rules.md` to understand task requirements.

Key rules to enforce:
- NO tasks marked as "optional"
- Every task MUST have file path
- Testing phase is MANDATORY
- Verb-based task descriptions
- Minimum 3 tasks total

### Step 2: Read Specification

1. Read `.claude/specs/{spec-id}/spec.md`
2. If not found: Show error "Spec not found: {spec-id}"
3. Extract:
   - Feature overview
   - Requirements (FR-xxx, NFR-xxx)
   - Acceptance criteria
   - Technical notes

### Step 3: Plan Task Breakdown

Use Claude's task planning capabilities to break down the spec into:

1. **Setup tasks** - Prerequisites, dependencies, configuration
2. **Implementation tasks** - Core functionality, one task per file/component
3. **Testing tasks** - Tests for each component

For each task:
- Clear description (action-oriented: "Create...", "Add...", "Implement...")
- Specific file path where changes will be made
- Logical ordering with dependencies

### Step 4: Generate tasks.md

1. Read template from `.claude/templates/tasks.template.md`
2. Fill with actual tasks organized by phase

3. **VALIDATE TASKS** against `.claude/rules.md`:
   - NO tasks marked as "optional"
   - ALL tasks have file paths (- file: path)
   - Testing phase exists and has tasks
   - All tasks are verb-based (Create/Add/Implement/Update/Test)
   - Minimum 3 tasks total

   If validation fails: Show error and DO NOT save. Regenerate tasks.

4. Save to `.claude/specs/{spec-id}/tasks.md`

### Step 5: Confirm

```
✓ Implementation tasks created!

Spec ID: {spec-id}
Tasks: {count} tasks across {phase-count} phases
Location: .claude/specs/{spec-id}/tasks.md

Next step: Review tasks.md, then run /spec-implement {spec-id} to start implementation
```

## Task Planning Guidelines

- **Be specific**: "Create User model in app/Models/User.php" not "Add user functionality"
- **One file per task** when possible
- **Include file paths**: Always specify where changes will be made
- **Logical order**: Dependencies first, then implementation, then tests
- **Granular**: Break large tasks into smaller checkboxes
- **Testable**: Each task should have clear completion criteria

## Example Output

```markdown
# Implementation Tasks: JWT Authentication

## Phase 1: Setup
- [ ] Install JWT library (tymon/jwt-auth) - file: composer.json
- [ ] Publish JWT config - file: config/jwt.php
- [ ] Generate JWT secret key - file: .env

## Phase 2: Implementation
- [ ] Create auth middleware - file: app/Http/Middleware/JwtAuth.php
- [ ] Add login endpoint - file: app/Http/Controllers/AuthController.php
- [ ] Add token refresh endpoint - file: app/Http/Controllers/AuthController.php

## Phase 3: Testing
- [ ] Test login flow - file: tests/Feature/AuthTest.php
- [ ] Test token refresh - file: tests/Feature/AuthTest.php
```
