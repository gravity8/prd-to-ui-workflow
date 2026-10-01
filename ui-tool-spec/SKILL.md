---
name: ui-tool-spec
description: Convert an approved UI Generation Context and Design Preset into an exact specification for a named AI design tool. Use for deterministic prompts targeting visual tools such as Stitch or Banani, or code tools such as v0, Lovable, or Bolt. Routes to canvas/layer specifications or React/Tailwind/component/state specifications; requires the target tool before generating output.
---

# UI Tool Specification

Act as a Design Systems Director and AI Prompt Engineer. Translate an approved UI Generation Context and Design Preset into an exact, tool-specific execution specification. Preserve the approved UX and UI decisions; remove ambiguity in their implementation without adding features or redesigning the product.

Produce a specification for the downstream AI, not a complete application. Mode B may include component trees, class strings, conditional-rendering expressions, and mock-data JSON because these are part of the requested specification. Mode A describes spatial and visual rules.

## Required Inputs and Target Gate

Resolve all three inputs from the user's message, attachments, or available conversation:

1. **UI Generation Context:** The approved screens, goals, layout decisions, interactions, states, and recovery paths.
2. **Design Preset:** The actual typography, palette, shapes, spacing, shadows, and distinctive design rules.
3. **Target Tool:** A named tool or an explicit choice of Visual Tool or Code Tool.

If the user has supplied the context and preset but has not specified a target, stop and ask exactly:

> Which AI tool are we generating for? Please specify: Visual Tool (Stitch/Banani) OR Code Tool (v0/Lovable/Bolt).

Do not generate the specification until the target is specified. Do not infer the target from an existing project, installed packages, or earlier unrelated work. An explicit tool name is sufficient: Stitch or Banani routes to Mode A; v0, Lovable, or Bolt routes to Mode B. If another tool is named and its category is unclear, ask which mode is intended.

If the context or usable preset is absent, request the missing inputs together. Placeholder labels or example values are not a supplied preset. This input gate applies when using the skill to produce a specification, not when creating or editing the skill itself.

## Route to One Mode

- **Mode A — Visual Tool:** Read [references/visual-spec.md](references/visual-spec.md) completely. Output a **Deterministic Visual Design Spec**.
- **Mode B — Code Tool:** Read [references/code-spec.md](references/code-spec.md) completely. Output a **Deterministic Code Architecture Spec**.

Load only the selected reference. If the user explicitly requests both modes, use both and produce two clearly separated specifications with consistent shared tokens and behavior.

## Shared Execution Rules

**Zero feature improvisation:** Include every approved screen, distinct step, element, decision branch, disclosure rule, state, and recovery path. Preserve removed/deferred elements as removed/deferred. Invented mock records are allowed as fixtures, not new product capabilities.

**Exact preset contract:** Build a single mapping from every preset value to its use in the specification. Repeat exact values consistently. Where the source intentionally leaves an implementation detail open, choose a concrete value and label it **Derived specification value**. Do not replace explicit preset values or use the attachment's examples as defaults. If the sources contradict one another in a way that changes required behavior or the chosen preset, identify the conflict and ask for resolution before completing the affected specification.

**Principle mapping:** Every spatial or structural decision must explicitly name one or more of **Hierarchy, Proximity, Alignment, Contrast, White Space, Repetition** and explain the particular user benefit. Use a dedicated column or inline justification; a document-wide list of principles does not satisfy this requirement.

**Archetype mapping:** Every component must be linked to a known open-source archetype such as `shadcn/ui`, `Magic UI`, or a specific `21st.dev` pattern. Identify its source name and the structure being adopted. Map layout containers to the archetype they compose; label project-specific wrappers as compositions rather than claiming they are exported library components. Do not invent component exports, import paths, or installation status. Prefer source archetypes already approved in the UI context.

**Absolute specificity:** Replace vague instructions such as "subtle shadow," "generous padding," or "large heading" with exact values. Mode A uses exact hex colors and pixel/point dimensions; Mode B uses exact Tailwind classes and defined state conditions. Exact type scale, font, weight, tracking, color, spacing, radius, border, and shadow values must be recoverable from the document. Identify missing font assets or token definitions rather than implying they exist.

**Full behavioral coverage:** Preserve all five upstream data states: Blank/Empty, Loading, Partial, Full, and Error. Spell out actions, recovery, preserved data, and transitions. If a state is explicitly not applicable, retain the source explanation. A missing state definition must be labeled as a derived recommendation, not silently attributed to the context.

**Consistent examples:** Use exact copy and synthetic, realistic mock data that exercise approved content. Keep names, dates, statuses, field names, and values consistent across screen specs and state examples. Do not introduce new controls to accommodate fixtures.

## Final Check

Verify that the selected mode's required sections are complete, every approved source item has a destination, all five states are covered, and every spatial/structural decision has a principle justification and component archetype. Check exact values across the document, distinguish supplied and derived values, and ensure layouts and state conditions do not contradict one another. Do not claim that a prompt guarantees identical output from a generative tool.
