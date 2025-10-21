# Specification & Task Governance Rules

**Purpose**: Ensure consistent, high-quality specifications and implementation tasks across all features.

## Critical Rules (MUST Enforce)

### Tests are Mandatory

- **Tests are REQUIRED for all features** - NO EXCEPTIONS
- NEVER mark tests as "optional" or "if time permits"
- NEVER skip testing phase
- Every spec MUST include test requirements
- Every task plan MUST include test tasks in Testing phase

### Requirements Format

- All functional requirements MUST use format: **FR-001**, **FR-002**, etc.
- All non-functional requirements MUST use format: **NFR-001**, **NFR-002**, etc.
- Minimum 3 functional requirements per spec
- Requirements must be specific and testable
- Each requirement must start with "System MUST" or "System SHOULD"

### Task Format

- NO tasks marked as "optional", "nice-to-have", or "if time permits"
- Every task MUST include: `- [ ] Description - file: path/to/file.ext`
- Tasks MUST be verb-based: "Create", "Add", "Implement", "Update", "Test"
- NO vague tasks like "Add functionality" or "Improve code"
- Minimum 3 tasks per implementation plan

## Quality Rules (SHOULD Enforce)

### Specification Structure

- Include "Out of Scope" section to clarify boundaries
- Acceptance criteria SHOULD use Given/When/Then format
- Technical notes MUST specify technology choices
- Overview must explain what, why, and how

### Task Organization

- Tasks organized into phases:
  - **Phase 1: Setup** - Dependencies, configuration, scaffolding
  - **Phase 2: Implementation** - Core feature code
  - **Phase 3: Testing** - Test creation and validation
- Testing phase MUST come after Implementation phase
- Each phase should have 2-5 tasks
- Tasks within a phase should be ordered by dependencies

### File Paths

- File paths must be specific: `app/Models/User.php` not `models folder`
- Use forward slashes: `src/components/Button.tsx`
- Include file extension
- Paths should be relative to project root

## Validation Checkpoints

### During /spec Generation

Before saving spec.md, verify:
- [ ] Tests are not marked optional
- [ ] At least 3 FR requirements with proper IDs
- [ ] At least 1 NFR requirement
- [ ] Acceptance criteria present
- [ ] Out of Scope section exists

### During /spec-plan Generation

Before saving tasks.md, verify:
- [ ] No tasks marked as optional
- [ ] All tasks have file paths
- [ ] Testing phase exists and has tasks
- [ ] All tasks are verb-based
- [ ] Minimum 3 tasks total

## Error Messages

If rules violated, show clear errors:

```
Rule Violation: Tests marked as optional

Found in spec: "Testing (optional)"

Tests are MANDATORY. Please regenerate spec with testing as required phase.
```

```
Rule Violation: Missing file path

Task: "Add authentication logic"
Missing: file path

Every task must specify where changes will be made.
Format: - [ ] Task description - file: path/to/file.ext
```

## Notes

- These rules apply to ALL specs and tasks, no exceptions
- Rules can be updated but changes should be committed to git
- Commands will automatically enforce these rules
- Manual specs should also follow these rules for consistency
