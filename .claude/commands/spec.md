# Generate Feature Specification

Create a specification document through interactive planning and clarification.

## User's Description

{PROMPT_ARGS}

## Workflow

This command uses PLAN MODE for interactive spec creation:

1. **Read governance rules** from `.claude/rules.md`
2. **Analyze the description** and identify what needs clarification
3. **Ask clarifying questions** using AskUserQuestion tool
4. **Discuss the approach** with the user
5. **Present the plan** showing what will be in the spec
6. **Wait for approval** via ExitPlanMode
7. **Generate spec** following rules
8. **Validate spec** against rules before saving
9. **Save spec** if validation passes

## Instructions for Plan Mode

### Phase 0: Read Governance Rules (REQUIRED)

**FIRST**: Read `.claude/rules.md` to understand quality requirements.

Key rules to enforce:
- Tests are MANDATORY (never optional)
- Requirements must have FR-xxx/NFR-xxx IDs
- Minimum 3 functional requirements
- Tasks need file paths
- Acceptance criteria format

### Phase 1: Clarification (REQUIRED)

1. Analyze the user's description
2. Identify ambiguities or missing information
3. Use AskUserQuestion to ask ALL clarifying questions at once:
   - Authentication requirements?
   - Data storage approach?
   - API endpoints and structure?
   - Integration points?
   - Performance requirements?
   - Scope boundaries?

4. Have discussion with user to understand their needs

### Phase 2: Plan Presentation (REQUIRED)

After clarifications, present a plan showing:

```
## Spec Plan for: {Feature Name}

### What will be built
- {Overview paragraph}

### Key Requirements
- FR-001: {requirement}
- FR-002: {requirement}
- NFR-001: {non-functional}

### Acceptance Criteria
- {criterion 1}
- {criterion 2}

### Technical Approach
- {tech stack}
- {architecture notes}

### Out of Scope
- {what's excluded}
```

Use ExitPlanMode to show this plan and wait for approval.

### Phase 3: Spec Generation (After Approval)

After user approves the plan:

1. Generate timestamp: `YYYY-MM-DD-HHMMSS`
2. Generate slug from description (kebab-case)
3. Create spec ID: `{timestamp}-{slug}`
4. Create folder: `.claude/specs/{spec-id}/`
5. Read template from `.claude/templates/spec.template.md`
6. Fill template with all the details discussed

7. **VALIDATE SPEC** against `.claude/rules.md`:
   - Tests are NOT marked as optional
   - At least 3 FR-xxx requirements
   - At least 1 NFR-xxx requirement
   - Requirements use "System MUST" format
   - Acceptance criteria present
   - Out of Scope section exists

   If validation fails: Show error and DO NOT save. Regenerate spec.

8. Save to `.claude/specs/{spec-id}/spec.md`
9. Confirm with:

```
✓ Specification created!

Spec ID: {spec-id}
Location: .claude/specs/{spec-id}/spec.md

Summary: {1-2 sentences}

Next step: Run /spec-plan {spec-id} to create implementation tasks
```

## Important Rules

- MUST use plan mode (you're already in it when this command runs)
- MUST ask clarifying questions before generating spec
- MUST use AskUserQuestion for user input
- MUST wait for ExitPlanMode approval before creating file
- NO placeholder answers - all clarifications resolved during planning
