# High Wizard Plan

## **PROJECT INFO**
- **Project**: agent-memory-system (control-files)
- **Date**: 2026-03-01
- **Agent**: Claude Meta
- **Theme**: Add brainstorming/ADR and bug-fix output types to high-wizard

---

## **OBJECTIVES**
Add 3 new optional section groups (E, F, G) to the high-wizard plan template and update the procedure to propose them. This restores the brainstorming/ADR and bug investigation capabilities from the deleted procedures (high-mountain, short-hill, fixing-rod, patching-ship) as optional sections within the existing single-template architecture.

### **Related Documents**
- [high-wizard.md](../control-files/procedure/high-wizard.md) - Procedure to update (Step 11 section proposal + Step 12 ADR creation)
- [high-wizard-plan-template.md](../control-files/plans/high-wizard-plan-template.md) - Template to add E/F/G sections
- [adr-template.md](../control-files/templates/adr-template.md) - ADR template referenced by section G
- [2026-02-28 Procedure Restructure Plan](completed/2026-02-28-control-files-procedure-restructure.md) - Previous restructure that created the gap

### **SUCCESS CRITERIA**
- [x] Plan template has optional sections E (Bug Investigation), F (Solution Options & Evaluation), G (ADR Output) with HTML comment markers
- [x] Procedure Step 11 proposes E/F/G alongside A-D based on task context
- [x] Procedure Step 12 includes ADR file creation instruction when G is confirmed
- [x] ADR template reference updated (stale footer cleaned if needed)
- [x] ARCHITECTURE.md updated with new optional sections
- [x] Grep for stale references passes (0 broken functional references)

---

## **SCOPE**

### In Scope
- Add optional sections E, F, G to high-wizard-plan-template.md
- Update high-wizard.md Step 11 (section proposal) to include E/F/G with proposal criteria
- Update high-wizard.md Step 12 to handle ADR file creation when G confirmed
- Update ARCHITECTURE.md protocol documentation
- Verify ADR template at templates/adr-template.md is clean

### Out of Scope
- Changing the core procedure flow (Steps 1-7 decision collection stays the same)
- Changing quick-wizard.md (it escalates to high-wizard, doesn't need these sections)
- Changing wide-ocean.md (orchestration layer, unaffected)
- Updating install scripts (no new files to install)
- Updating README.md, SETUP.md (no structural changes, just new optional sections within existing template)

---

## **CONFIRMED DECISIONS**
*These decisions were collected during investigation and confirmed by Alvi. The reasons serve as the analysis record.*

| # | Decision | Chosen | Reason |
|---|----------|--------|--------|
| 1 | Output type detection | Detect during investigation, propose at Step 11 | Investigation naturally reveals task type. Same mechanism as existing A-D optional sections. |
| 2 | Template strategy | Single template — add E, F, G optional section groups | ~80% of plan is common across all task types. Only Solution section varies. Same HTML marker pattern as A-D. |
| 3 | ADR output | Separate bonus file when G confirmed | ADRs serve as concise decision records for implementation agents. Separate file is established pattern. |
| 4 | Brainstorming depth (F) | Streamlined: Solution Options (5-8) + Evaluation (pros/cons) + Selected Approach | Wizard investigation already does deep analysis. Section F documents the evaluation, not the thinking process. |
| 5 | Bug fix depth (E) | Combined: Bug Info + Scaffolding Check + Bug Location + Hypothesis Testing + Root Cause | Keeps hypothesis-driven debugging (key innovation) while streamlining scaffolding and removing redundant replication section. |
| 6 | Procedure step handling | No branching — Step 11 proposes, Step 12 fills confirmed sections | Identical flow for all task types. No conditional steps needed. |
| 7 | ADR template location | Keep at templates/adr-template.md | Correct location for output templates used by procedures. |

---

## **SOLUTION**

### Architecture Overview

The high-wizard already follows a procedure → template architecture where the procedure guides the agent through steps, and the template provides the plan structure. This change extends both:

1. **Template** gains 3 new optional sections (E/F/G) using the same HTML comment marker pattern as existing A-D sections
2. **Procedure** Step 11 gains E/F/G proposal criteria; Step 12 gains ADR file creation when G is confirmed
3. **ADR template** at `templates/adr-template.md` becomes a referenced output template, triggered by section G

No new files are created. No procedure branching is needed. The agent proposes relevant sections at Step 11 based on what the investigation revealed, same as it already does for A-D.

### Component 1: Plan Template Sections E/F/G
- **Purpose**: Allow plans to capture bug investigation, solution options evaluation, and ADR output metadata
- **Key Files**: `control-files/plans/high-wizard-plan-template.md`
- **Design**:
  - **Section E (Bug Investigation)**: Bug Info + Scaffolding Check + Bug Location + Hypothesis Testing table + Root Cause. Placed after section D in the Solution area. The hypothesis table enforces sequential testing (key innovation from fixing-rod/patching-ship).
  - **Section F (Solution Options & Evaluation)**: Solution Options table (5-8 options) + Evaluation table (pros/cons of top candidates) + Selected Approach with rationale. Placed after section E.
  - **Section G (ADR Output)**: Lightweight section documenting which ADR was created and linking to it. Triggers ADR file creation in procedure Step 12. Placed after section F.

### Component 2: Procedure Updates
- **Purpose**: Enable the agent to detect task context and propose E/F/G alongside A-D, and create ADR files when needed
- **Key Files**: `control-files/procedure/high-wizard.md`
- **Design**:
  - **Step 11 addition**: Add E/F/G to the optional sections list with proposal criteria (bug fix → E, brainstorming/decisions → F, architectural decisions → G). G depends on F.
  - **Step 12 addition**: After filling confirmed optional sections, if G is confirmed, copy the ADR template and fill it using content from section F and the Confirmed Decisions table. Link ADR back to the plan.

### Component 3: Documentation Updates
- **Purpose**: Keep ARCHITECTURE.md and ADR template aligned with new capabilities
- **Key Files**: `control-files/ARCHITECTURE.md`, `control-files/templates/adr-template.md`
- **Design**:
  - **ARCHITECTURE.md**: Verify Wizard Protocols section description covers E/F/G (it was pre-written during restructure — validate accuracy)
  - **ADR template**: Clean stale "brainstorming plan file" link text/path to reference "High Wizard plan file" with correct naming convention

### Integration Architecture

| Component | Integrates With | Data Flow | Dependencies |
|-----------|----------------|-----------|--------------|
| Plan Template (E/F/G) | Procedure Step 11 | Step 11 proposes sections → user confirms → Step 12 fills confirmed sections | Existing HTML marker pattern (A-D) |
| Procedure Step 11 | Plan Template | Investigation findings → section proposal with criteria | Investigation step (Step 5) reveals task type |
| Procedure Step 12 | ADR Template | When G confirmed: copy ADR template → fill from F + decisions → link back to plan | Section F content + Confirmed Decisions table |
| ADR Template | Procedure Step 12 | Template file → filled ADR output file | Must exist at `templates/adr-template.md` |
| ARCHITECTURE.md | None (documentation) | Reflects current capabilities | Updated after template + procedure changes |

---

## **IMPLEMENTATION PHASES**

### Phase 1: Plan Template — Add Optional Sections E, F, G
- [ ] **Step 1.1**: Add section E (Bug Investigation) to template
  - **Action**: Add HTML comment marker and section content for Bug Investigation after section D
  - **Implementation**: Insert `<!-- OPTIONAL SECTION E -->` block with subsections: Bug Information (report, context, severity), Scaffolding Check (existing tests, debugging tools, reproduction), Bug Location (suspected area, evidence), Hypothesis Testing (sequential table: #, hypothesis, test, result, confirmed), Root Cause (confirmed cause, evidence)
  - **Testing**: Read template file and verify E section is present with correct HTML marker and all 5 subsections
  - **Success Criteria**: Section E appears after D with `<!-- OPTIONAL SECTION E: ... -->` marker and all 5 subsections

- [ ] **Step 1.2**: Add section F (Solution Options & Evaluation) to template
  - **Action**: Add HTML comment marker and section content for Solution Options & Evaluation after section E
  - **Implementation**: Insert `<!-- OPTIONAL SECTION F -->` block with subsections: Solution Options table (#, solution, description — for 5-8 options), Evaluation table (solution, pros, cons — for top candidates), Selected Approach (chosen solution, rationale connecting evidence from evaluation)
  - **Testing**: Read template file and verify F section is present with correct marker and all 3 subsections
  - **Success Criteria**: Section F appears after E with `<!-- OPTIONAL SECTION F: ... -->` marker and all 3 subsections

- [ ] **Step 1.3**: Add section G (ADR Output) to template
  - **Action**: Add HTML comment marker and section content for ADR Output after section F
  - **Implementation**: Insert `<!-- OPTIONAL SECTION G -->` block with: instruction note referencing the ADR Template path, ADR File path placeholder, Decision Summary placeholder. Include note that procedure Step 12 handles actual ADR file creation.
  - **Testing**: Read template file and verify G section is present with correct marker and ADR template reference
  - **Success Criteria**: Section G appears after F with `<!-- OPTIONAL SECTION G: ... -->` marker and ADR template reference link

### Phase 2: Procedure — Update Steps 11 and 12
- [ ] **Step 2.1**: Update Step 11 with E/F/G section proposal criteria
  - **Action**: Add E, F, G entries to the optional sections list in Step 11
  - **Implementation**: Add after the D entry: `E) Bug Investigation` (propose when: bug fix, debugging, error investigation, unexpected behavior), `F) Solution Options & Evaluation` (propose when: brainstorming/decision tasks, multiple viable approaches, architecture decisions), `G) ADR Output` (propose when: F is included AND decision has architectural significance worth documenting separately). Update the response format example to show E/F/G entries.
  - **Testing**: Read procedure file and verify E/F/G appear in Step 11 with proposal criteria and response format
  - **Success Criteria**: Step 11 lists A-G with clear proposal criteria for each

- [ ] **Step 2.2**: Update Step 12 with ADR file creation instruction
  - **Action**: Add ADR file creation instruction to Step 12 for when section G is confirmed
  - **Implementation**: Add after the existing "Optional sections" paragraph: "**ADR file creation**: If section G is confirmed, after filling all plan sections: 1) Copy the [ADR Template](//@agent-memory/control-files/templates/adr-template.md), 2) Fill using content from section F and Confirmed Decisions, 3) Link ADR back to this plan file, 4) Update plan's section G with the ADR file path."
  - **Testing**: Read procedure file and verify Step 12 includes ADR creation instruction with 4 sub-steps
  - **Success Criteria**: Step 12 has ADR creation instruction that triggers only when G is confirmed

### Phase 3: Documentation & Verification
- [ ] **Step 3.1**: Update ARCHITECTURE.md
  - **Action**: Verify and update Wizard Protocols section to accurately reflect E/F/G capabilities
  - **Implementation**: The High Wizard description was pre-written during restructure to say "adapts to any task (planning, analysis, brainstorming, bug investigation)". Verify this matches reality now that E/F/G exist. Check if the Universal RAS Triggers table references deleted protocols — if so, note as tech debt (CLAUDE.md stale triggers are a separate cleanup task, out of scope). Ensure no other stale references exist in the file.
  - **Testing**: Read ARCHITECTURE.md and verify High Wizard description is accurate, no stale functional references
  - **Success Criteria**: ARCHITECTURE.md accurately describes High Wizard's capabilities; any stale references noted as tech debt

- [ ] **Step 3.2**: Clean ADR template stale references
  - **Action**: Update the link text and path pattern in adr-template.md
  - **Implementation**: Change `**Full brainstorming context**: [Link to brainstorming plan file](../../plans/[date]-[project]-[theme]-brainstorm.md)` to `**Full context**: [Link to High Wizard plan file](../../plans/[date]-[project]-[theme].md)`. Verify footer text says "Architecture Decision Records" (not "High Mountain Protocol").
  - **Testing**: Read ADR template and verify no stale references to deleted procedures or old naming conventions
  - **Success Criteria**: ADR template has no references to deleted procedures, link text matches current naming

- [ ] **Step 3.3**: Grep verification for stale references
  - **Action**: Search all active control-files for stale references to deleted procedures
  - **Implementation**: Grep for: `high-mountain`, `short-hill`, `fixing-rod`, `patching-ship`, `deep-trench`, `shallow-shore`, `quick-surf`, `brainstorm.md` across all `.md` files in `control-files/`. Exclude changelog and archive files.
  - **Testing**: Each grep returns 0 functional references (changelog/archive/history mentions are OK)
  - **Success Criteria**: 0 broken functional references to deleted procedures in any active control file

---

## **EXECUTION LOG**
**Execution Protocol for AI**:
I have to use this document as my **ONLY** source of truth to execute and track the plan steps iteratively. I should **NOT** use additional tools like ToDos because it lacks the context of what should I do. Everytime I want to implement a step I have to check the reference to the original step plan above. Everytime a step has been finished I need to go back to this document to log what was done.
*In other words*:
- I have to make this document as the source of truth for the implementation phase on what I have worked on and what I will be working
- The original plan must be fully in my context, therefore, I have to make sure I loaded the **Plan File** before executing any task and read carefully the reference to the original step
- I have to do the implementation by doing it in order per step THEN, I ALWAYS have to fill the step log rightly after

**Definition of Done (applies to ALL steps)**:
- ✅ **Code Quality**: Code compiles/runs without errors
- ✅ **Testing**: Tests written and passing
- ✅ **Logged**: Implementation and testing logged below
- 🚫 **Blocked**: Get input from [USER-NAME] before assuming

### Phase 1: Plan Template — Add Optional Sections E, F, G
- [x] **Step 1.1**: [Add section E to template](#step-11-add-section-e-bug-investigation-to-template)
  - **Implementation Log**: Added `<!-- OPTIONAL SECTION E: Include for bug investigation/fix tasks -->` block at line 109 of high-wizard-plan-template.md, after section D. Contains 5 subsections: Bug Information (report/context/severity), Scaffolding Check (tests/tools/reproduction), Bug Location (area/evidence), Hypothesis Testing (sequential table with #/hypothesis/test/result/confirmed columns), Root Cause (cause/evidence).
  - **Testing Log**: Read template lines 93-142. Verified: E marker present at line 109, all 5 subsections present, correctly placed between D and `---` separator before IMPLEMENTATION PHASES.
  - **Success Criteria**: Pass — section E appears after D with correct HTML marker and all 5 subsections
  - **Result**: Complete

- [x] **Step 1.2**: [Add section F to template](#step-12-add-section-f-solution-options--evaluation-to-template)
  - **Implementation Log**: Added `<!-- OPTIONAL SECTION F: Include for brainstorming/decision tasks, multiple viable approaches -->` block at line 139 of high-wizard-plan-template.md, after section E. Contains 3 subsections: Solution Options (table with 5 rows: #/solution/description), Evaluation (table: solution/pros/cons for top 3 candidates), Selected Approach (chosen/rationale).
  - **Testing Log**: Read template lines 135-174. Verified: F marker present at line 139, all 3 subsections present, correctly placed between E and `---` separator before IMPLEMENTATION PHASES.
  - **Success Criteria**: Pass — section F appears after E with correct HTML marker and all 3 subsections
  - **Result**: Complete

- [x] **Step 1.3**: [Add section G to template](#step-13-add-section-g-adr-output-to-template)
  - **Implementation Log**: Added `<!-- OPTIONAL SECTION G: Include when task produces an architecture decision record -->` block at line 166 of high-wizard-plan-template.md, after section F. Contains: instruction note with ADR Template link (`../templates/adr-template.md`), ADR File path placeholder (filled by procedure Step 12), Decision Summary placeholder.
  - **Testing Log**: Read template lines 162-181. Verified: G marker present at line 166, ADR template reference link present and correct, both placeholders present, correctly placed before `---` separator and IMPLEMENTATION PHASES.
  - **Success Criteria**: Pass — section G appears after F with correct HTML marker and ADR template reference link
  - **Result**: Complete

### Phase 2: Procedure — Update Steps 11 and 12
- [x] **Step 2.1**: [Update Step 11 with E/F/G criteria](#step-21-update-step-11-with-efg-section-proposal-criteria)
  - **Implementation Log**: Added 3 entries to the optional sections list in Step 11 of high-wizard.md: E) Bug Investigation (bug fix, debugging, error investigation), F) Solution Options & Evaluation (brainstorming, multiple approaches, architecture decisions), G) ADR Output (F included AND architectural significance). Updated response format example to show all 7 entries (A-G).
  - **Testing Log**: Read procedure lines 89-123. Verified: all 7 entries A-G present with proposal criteria (lines 94-100), response format shows all 7 checkbox entries (lines 107-113).
  - **Success Criteria**: Pass — Step 11 lists A-G with clear proposal criteria for each
  - **Result**: Complete

- [x] **Step 2.2**: [Update Step 12 with ADR creation](#step-22-update-step-12-with-adr-file-creation-instruction)
  - **Implementation Log**: Updated "Optional sections" range from A-D to A-G in Step 12. Added "ADR file creation" paragraph with 4 numbered sub-steps: 1) copy ADR template, 2) fill from section F + decisions, 3) link back to plan, 4) update plan's section G with path. ADR template link uses `//@agent-memory/control-files/templates/adr-template.md`.
  - **Testing Log**: Read procedure lines 120-139. Verified: A-G range at line 124, ADR creation instruction with 4 sub-steps at lines 126-130, ADR template link correct, CRITICAL paragraph preserved after.
  - **Success Criteria**: Pass — Step 12 has ADR creation instruction that triggers only when G is confirmed
  - **Result**: Complete

### Phase 3: Documentation & Verification
- [x] **Step 3.1**: [Update ARCHITECTURE.md](#step-31-update-architecturemd)
  - **Implementation Log**: Verified Wizard Protocols section (lines 292-319). High Wizard description already says "adapts to any task (planning, analysis, brainstorming, bug investigation)" and "Smart planning with dynamic section proposal" — accurate now that E/F/G exist. No changes needed.
  - **Testing Log**: Read ARCHITECTURE.md lines 196-220. Wizard Protocols section matches implemented capabilities. RAS triggers table (lines 209-211) lists Deep Trench, Shallow Shore, Quick Surf — stale but reflects current CLAUDE.md state.
  - **Success Criteria**: Pass — ARCHITECTURE.md accurately describes High Wizard's capabilities
  - **Tech Debts**: RAS triggers table lists 3 deleted protocols (Deep Trench/Shallow Shore/Quick Surf) that still exist in CLAUDE.md's `2-core-ras-memory.md`. Separate cleanup task needed to remove stale triggers from CLAUDE.md, then update ARCHITECTURE.md table.
  - **Result**: Complete — no changes required, tech debt noted

- [x] **Step 3.2**: [Clean ADR template stale references](#step-32-clean-adr-template-stale-references)
  - **Implementation Log**: Updated line 53 of adr-template.md: changed "Full brainstorming context" → "Full context", "Link to brainstorming plan file" → "Link to High Wizard plan file", removed `-brainstorm` suffix from path pattern (`[theme]-brainstorm.md` → `[theme].md`). Footer already clean: "Architecture Decision Records" + "High Wizard/Quick Wizard".
  - **Testing Log**: Grep for `brainstorm|high.mountain|short.hill|fixing.rod|patching.ship` in adr-template.md → 0 matches. No stale references remain.
  - **Success Criteria**: Pass — ADR template has no references to deleted procedures, link text matches current naming
  - **Result**: Complete

- [x] **Step 3.3**: [Grep verification](#step-33-grep-verification-for-stale-references)
  - **Implementation Log**: Ran 3 grep searches across all `.md` files in `control-files/`: 1) `high-mountain|short-hill|fixing-rod|patching-ship`, 2) `deep-trench|shallow-shore|quick-surf`, 3) `brainstorm\.md`.
  - **Testing Log**: Results: 0 broken functional references in active control files (procedure/, plans/, templates/, ARCHITECTURE.md). Found: core-instruction-control-files.md:221 has historical reasoning memory mention of "shallow-shore and deep-trench" — not a functional link, past lesson record. core-memory/compiled/core-memory-compiled.md has 7 stale RAS trigger links — generated artifact, same tech debt as Step 3.1. `brainstorm.md` pattern: 0 matches.
  - **Success Criteria**: Pass — 0 broken functional references to deleted procedures in active control files
  - **Tech Debts**: Same as Step 3.1: stale RAS triggers in `2-core-ras-memory.md` (source) → `compiled/core-memory-compiled.md` (generated) → CLAUDE.md (installed). Separate cleanup task.
  - **Result**: Complete

---

## **POST-COMPLETION**
After all phases are executed and logged, move this plan to `plans/completed/`:
- **Windows**: `powershell -c "if (!(Test-Path './plans/completed')) { New-Item -ItemType Directory -Path './plans/completed' -Force }; Move-Item './plans/2026-03-01-control-files-high-wizard-output-types.md' './plans/completed/2026-03-01-control-files-high-wizard-output-types.md' -Force"`
- **Linux/macOS**: `mkdir -p ./plans/completed && mv ./plans/2026-03-01-control-files-high-wizard-output-types.md ./plans/completed/2026-03-01-control-files-high-wizard-output-types.md`
