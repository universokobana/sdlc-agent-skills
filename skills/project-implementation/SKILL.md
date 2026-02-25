---
name: project-implementation
description: Implement a project from its documentation and specification. Use when asked to "implement project", "continue implementation", "build from docs", "implement from spec", or when the user wants to progressively implement a documented project following a todo checklist. Reads docs/, creates implementation plans and todo lists, and implements incrementally with tests and commits.
---

# Project Implementation

## Overview

Progressively implement a project that is documented and specified in `docs/`. Work through a structured todo list, implementing one phase/section at a time, running tests, committing, and updating progress tracking files after each step.

**Core principle:** Never skip tests. Never mark a task as done without verified implementation. Always commit after each completed section. Always update tracking files before moving to the next task.

## The Process

### Phase 1: Read Project Documentation

1. **Read all files in `docs/`**

   ```bash
   find docs/ -type f -name '*.md' | sort
   ```

   Read every documentation file to understand the full project scope, architecture, and requirements.

2. **Read `docs/implementation.md`** (Implementation Plan)

   - If it **exists** → read it carefully to understand the phases, order of execution, and dependencies
   - If it **does NOT exist** → create it from the specification files in `docs/`:
     - Analyze all spec documents
     - Break the project into logical implementation phases (Phase 0: Setup, Phase 1: Core, Phase 2: Features, etc.)
     - Each phase should have clear deliverables and acceptance criteria
     - Write the plan to `docs/implementation.md`

3. **Read `docs/todo.md`** (Task Checklist)

   - If it **exists** → read it to understand what needs to be done
   - If it **does NOT exist** → create it from `docs/implementation.md`:
     - Convert each phase into a section with checkbox items
     - Each item should be a single, atomic, implementable task
     - Use the format `- [ ]` for pending and `- [x]` for completed
     - Group by phase, with clear section headers
     - Example structure:

       ```markdown
       # Project Name — TODO

       ---

       ## Phase 0 — Setup

       ### Initialization
       - [ ] Create `package.json`
       - [ ] Create `tsconfig.json`
       - [ ] Create `.gitignore`

       ### Build
       - [ ] Install dev dependencies
       - [ ] Create build config
       - [ ] Validate `npm run build` works
       - [ ] Validate `npm run test` works

       ### Directory Structure
       - [ ] Create `src/` directories
       - [ ] Create `__tests__/` directories

       ---

       ## Phase 1 — Core Feature

       ### Sub-feature A
       - [ ] Implement X
       - [ ] Implement Y
       - [ ] Write tests for X and Y
       ```

4. **Read `docs/implemented.md`** (Implementation Log)

   - If it **exists** → read it to understand what was already done and where to resume
   - If it **does NOT exist** → create it with this initial content:

     ```markdown
     # Implementation Log

     > Auto-updated after each implementation cycle.

     ---
     ```

### Phase 2: Determine Where to Resume

1. Compare `docs/todo.md` with `docs/implemented.md`
2. Find the **first unchecked item** (`- [ ]`) in `todo.md`
3. That is the starting point for this session

### Phase 3: Implementation Loop

For **each unchecked section/group** in `todo.md`, repeat:

#### 3a. Implement

- Read the task description
- Implement the minimum required to complete all items in the current section/group
- Follow project conventions found in the documentation
- Stay focused on the scope — no "while I'm here" changes

#### 3b. Run Tests

```bash
# Run the project's test command (detect from package.json, Makefile, etc.)
npm run test
# or
bundle exec rspec
# or
pytest
# or whatever the project uses
```

- All tests MUST pass before proceeding
- If tests fail, fix them before moving on
- If the section introduces new behavior, write tests for it

#### 3c. Commit

```bash
git add <changed files>
git commit -m "feat: <description of what was implemented>

Co-Authored-By: Claude <noreply@anthropic.com>"
```

- One commit per completed section/group
- Use conventional commits: `feat:`, `fix:`, `chore:`, `refactor:`, `test:`
- Commit message in the project's language (follow existing commit style)

#### 3d. Update `docs/todo.md`

Mark all completed items as done:

```markdown
- [x] Create `package.json`  ← was `- [ ]`
```

#### 3e. Update `docs/implemented.md`

Append a summary of what was implemented:

```markdown
## Phase 0 — Setup > Initialization

- Created `package.json` with scope `@project/name`
- Created `tsconfig.json` targeting ES2022
- Created `.gitignore`

**Commit:** `abc1234`
```

#### 3f. Clear Context and Restart

After updating tracking files:

1. **Commit the tracking file updates**:
   ```bash
   git add docs/todo.md docs/implemented.md
   git commit -m "docs: update implementation progress

   Co-Authored-By: Claude <noreply@anthropic.com>"
   ```

2. **Stop and restart the process from Phase 1**
   - This ensures fresh context for the next section
   - Prevents context window overflow on large projects
   - Each cycle is self-contained: read → implement → test → commit → update → restart

### Phase 4: Completion

When all items in `todo.md` are checked (`- [x]`):

1. Run the full test suite one final time
2. Update `docs/implemented.md` with a completion summary
3. Inform the user that implementation is complete

## Quick Reference

| Step | Action | Success Criteria |
|------|--------|-----------------|
| 1. Read docs | Load all project documentation | Full understanding of scope |
| 2. Plan | Create/read implementation.md | Clear phased plan exists |
| 3. Todo | Create/read todo.md | Granular checklist exists |
| 4. Resume | Find first unchecked item | Know where to start |
| 5. Implement | Code the current section | All items in section done |
| 6. Test | Run tests | All tests pass |
| 7. Commit | Git commit the implementation | Clean commit history |
| 8. Track | Update todo.md + implemented.md | Progress recorded |
| 9. Restart | Clear context, go to step 1 | Fresh context for next cycle |

## Red Flags — STOP and Reassess

- Implementing without reading ALL docs first
- Skipping test execution after implementation
- Marking tasks done without actually implementing them
- Making changes outside the scope of the current section
- Committing without running tests
- Not updating tracking files after each cycle
- Trying to implement everything in one cycle (risk of context overflow)
- Moving to the next section when tests are failing

**STOP. Follow the process.**

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "This section is trivial, skip tests" | Every implementation needs test verification. |
| "I'll update todo.md at the end" | Update after EACH section, not after all. |
| "I'll do multiple sections before committing" | One commit per section keeps history clean. |
| "Tests aren't set up yet, skip them" | Setting up tests IS part of Phase 0. |
| "I remember what was done, skip reading docs" | Always re-read — context may have been cleared. |
| "The todo is too granular" | Granular tasks = clear progress + clean commits. |

## Notes

- **Always re-read docs at the start of each cycle** — context may have been compressed or cleared
- **One section per cycle** — keeps commits atomic and context fresh
- **The todo.md is the source of truth** — if it's not checked, it's not done
- **The implemented.md is the audit log** — always record what was done and the commit hash
- **Detect the project's tech stack** from docs and existing files to use the correct test/build commands
