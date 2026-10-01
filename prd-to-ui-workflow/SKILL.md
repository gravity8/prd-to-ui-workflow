---
name: prd-to-ui-workflow
description: Orchestrate zero-designer-ux, ux-to-ui-blueprint, and ui-tool-spec in sequence to turn a PRD, design preset, and named target tool into complete UX architecture, a UI Generation Context, and a tool-ready specification. Use for the full PRD-to-UI planning workflow or an explicit request to coordinate these three skills. Produces design handoff documents, not an application.
---

# PRD-to-UI Workflow

Run the user's three design skills as one continuous workflow. Pass each complete artifact directly into the next stage so the user does not have to invoke the skills separately or copy their outputs between steps.

This skill coordinates the workflow; the referenced skills remain the source of truth for their stage instructions. Execute the stages sequentially in the current task. Loading and applying their instructions is the orchestration mechanism; do not assume there is a separate skill-invocation API.

## Inputs

Resolve from the user's message, attachments, files, or available conversation:

- **PRD:** The complete product requirements and core user goal.
- **Design Preset:** Actual typography, palette, shape, spacing, shadow, and other supplied visual rules.
- **Target Tool:** Stitch/Banani or an explicit Visual Tool choice; v0/Lovable/Bolt or an explicit Code Tool choice. For another named tool, clarify its mode if necessary.
- **Output Location:** Use the user's chosen location when provided; otherwise use a unique task-local artifact directory if file tools are available.

Do not mistake bracketed examples for a preset, skill instructions for a PRD, or a skill-creation confirmation for a completed design artifact. This input process applies when running the workflow, not when creating or editing this skill.

Collect missing inputs together and preserve useful progress:

- Without a PRD or an explicitly supplied valid resume artifact, request the missing source before starting.
- Without a usable preset, Stage 1 can proceed, but Stage 2 cannot.
- Without a target tool, Stages 1 and 2 can proceed when their inputs are present, but Stage 3 cannot.
- If the UI context and preset are available and only the target is missing, ask exactly: **Which AI tool are we generating for? Please specify: Visual Tool (Stitch/Banani) OR Code Tool (v0/Lovable/Bolt).**

Ask only for information that is missing or materially changes the result. Do not add routine approval checkpoints between completed stages. When all inputs are present, run the entire workflow without waiting for separate stage-by-stage requests. If the user asks to review at a particular checkpoint, honor that pause.

## Stage Routing

| Stage | Load and apply | Complete inputs | Output |
| --- | --- | --- | --- |
| 1 — UX architecture | [zero-designer-ux](../zero-designer-ux/SKILL.md) | Full PRD | `01-ux-architecture.md` |
| 2 — UI translation | [ux-to-ui-blueprint](../ux-to-ui-blueprint/SKILL.md) | Complete Stage 1 artifact + preset | `02-ui-generation-context.md` |
| 3 — Target specification | [ui-tool-spec](../ui-tool-spec/SKILL.md) | Complete Stage 2 artifact + same preset + explicit target | `03-tool-specification.md` |

Read the current stage's `SKILL.md` completely before executing that stage, including required references. In Stage 3, load only the selected Visual or Code mode reference unless the user explicitly requests both.

The links resolve to sibling skill folders in the installed skills directory. If a path is stale, locate the matching skill by name in the available catalog. If a required skill is unavailable, preserve completed artifacts and report the missing dependency before its stage. Do not silently substitute a summarized copy of its framework.

### Stage 1 — PRD to UX Architecture

Apply all four steps of `zero-designer-ux`, including the JTBD audit, OOUX diagram and text hierarchy, behavioral flows and five-state coverage, and cognitive-load cancellation audit.

Complete its verification before proceeding. Preserve feature, screen, and step IDs, V1/deferred decisions, recovery behavior, and the distinction between requirements, implications, and assumptions. Carry unresolved research hypotheses forward; do not treat them as validated findings.

### Stage 2 — UX Architecture to UI Generation Context

Apply `ux-to-ui-blueprint` to the FULL Stage 1 artifact and the user's preset. Do not use an executive summary as its source.

Retain IDs and map every behavioral insight, decision, state, cancellation, relocation, and recovery to a UI directive. Keep supplied preset values and derived recommendations distinguishable. Preserve its required global rules, per-screen blueprint, navigation logic, and coverage ledger.

The workflow request authorizes producing this stage from the previous stage's output. Do not describe either generated document as human-approved unless the user has actually approved it.

### Stage 3 — UI Context to Tool-Ready Specification

Apply `ui-tool-spec` using the FULL Stage 2 artifact, the original preset, and the explicit target. Preserve the complete preset-to-token mapping from Stage 2 alongside the original values, so aliases and derived details do not change during translation.

- **Visual mode:** Produce the required canvas/grid, layer-by-layer screens, exact copy/mock data, and state visualizations.
- **Code mode:** Produce the required tech/component strategy, component trees and Tailwind specifications, five-state rendering logic, and mock data/interactions.

Preserve the selected mode's complete output structure and every applicable state. Short code architecture annotations are permitted only where Stage 3 Code mode calls for them. This workflow does not authorize building an app or submitting prompts to external tools.

## Handoff Integrity

Maintain one source register throughout the workflow: PRD source/revision, preset source/revision, target, completed artifact paths or headings, and unresolved dependencies. Keep it as a short handoff note within the output package rather than creating unrelated tracking files.

At each handoff, check the stage's own quality requirements and the following cross-stage invariants:

- The core user goal and retained feature scope do not change.
- IDs, object names, screen names, and decision destinations remain traceable.
- Every screen or distinct step accounts for Blank/Empty, Loading, Partial, Full, and Error, including explicit not-applicable explanations.
- Primary-action hierarchy, cancelled elements, relocation destinations, and recovery paths survive the translation.
- Preset values and derived token mappings remain consistent.
- Assumptions, proposed exceptions, and open questions do not become approved facts.

Repair a translation omission in the stage that introduced it, then refresh any affected downstream artifact. If resolving a conflict would change the product goal, a mandatory requirement, or an explicit preset choice, ask for the necessary decision before proceeding with dependent work. Do not manufacture a resolution to complete the pipeline.

## Delivery, Resume, and Revisions

Produce all three complete Markdown documents. If file tools are available, save them in the user-selected directory or a unique directory such as `artifacts/prd-to-ui/<run-name>/`, using normal file-editing tools. Avoid overwriting unrelated or user-edited files. Deliver a concise final response with links to the three documents, the chosen target, and any material open decisions. This concise message is a delivery note, not a replacement for the full artifacts.

If file output is unavailable, deliver the three complete documents in clearly labeled sections. Do not compress away mandatory screens, states, or recovery paths to fit a short answer. If a response limit requires splitting delivery, keep the complete artifacts and report the exact remaining stage rather than claiming completion.

When blocked on input, identify what is complete, what is waiting, and which input unlocks the next stage. Resume from the first incomplete stage once the user supplies it; do not repeat completed work unless its source changes.

Reuse an existing artifact only when it is complete, belongs to the same product/revision, and the user supplies or identifies it for the workflow. Read the full artifact, not just its heading or summary.

For requested changes, regenerate only the affected stage and its dependents: PRD changes affect Stages 1–3; preset changes affect Stages 2–3; target changes affect Stage 3. Preserve unaffected valid artifacts and track which outputs replace earlier revisions.
