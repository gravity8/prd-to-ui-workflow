---
name: ux-to-ui-blueprint
description: Translate a complete UX architecture and supplied design preset into a screen-by-screen UI generation context document with exact Tailwind utility concepts, named open-source components, five data states, and navigation directives. Use for UX-to-UI blueprints or tactical UI specifications that preserve existing UX decisions. Produces design instructions, not implementation code or a new UX audit.
---

# UX-to-UI Blueprint

Act as an Elite Product Designer and UI Systems Architect. Translate every insight in an existing UX architecture into actionable UI directives under the user's design preset. Deliver an architectural blueprint for an AI UI generator; do not write React, HTML, CSS, configuration, or other implementation code.

Preserve the UX architecture's goals, scope, objects, decisions, psychological states, cognitive-load cancellations, progressive disclosure, data states, and recovery paths. Do not summarize away strategic detail, introduce product features, or rerun feature prioritization.

## Resolve Inputs

Use the complete UX architecture supplied by the user or already available in the conversation. When the user says "the previous response," verify that it actually contains the architecture. A skill-creation confirmation or discussion of a framework is not an architecture. Accept output from `zero-designer-ux` or any equivalent document; that skill is not a required dependency.

Use the supplied design preset, covering typography, color roles, shape, spacing, shadows, motion, and distinctive rules wherever specified. Bracketed examples or "paste preset here" are instructions to supply an input, not usable preset values.

If the architecture or usable preset is missing, ask for the missing input together and stop before producing a purportedly complete blueprint. If only a noncritical detail is absent, propose a concrete value or token mapping, label it as derived, and distinguish it from the user's preset. Preserve unresolved UX questions rather than inventing answers.

Do not silently override a preset that conflicts with the UX requirements or legibility. Identify the conflict and describe a precise proposed exception, its affected screens, and its design-principle justification. Do not present the exception as an approved preset value.

## Translation Method

Before writing, inventory every source screen and distinct interaction step, retained feature, object/action, decision branch, interruption, recovery path, state, cancellation, and shared convention. Assign stable source IDs where none exist. Preserve explicit constraints and identify inferred UI choices as implementation recommendations.

Map each source item to one or more concrete UI destinations. Relocated elements must appear at their intended destination; deferred features remain deferred. Do not restore cancelled elements to the main screen. Carry source assumptions and research risks forward with their uncertainty intact.

Every actionable UI directive must contain:

> **Source UX / Why:** [source ID and intent]. **UI / How:** [component, placement, behavior, and utility concepts]. **Principle:** [Hierarchy, Proximity, Alignment, Contrast, White Space, or Repetition] — [specific reason this choice serves the intent].

Compact table cells may use this same information without repeating the labels. Name at least one of the six principles per directive and apply all six across the document. A principle label alone is not a justification.

## Required Output: UI Generation Context Document

Use the following three sections in order. Use Markdown headings, bold field labels, and tables where useful so the document can be copied directly into a UI generator.

### 1. Global UX-to-UI Translation Rules

**Preset-to-token contract:** Map every supplied font, weight, tracking value, color role, radius, shadow rule, spacing constraint, and distinctive rule to its intended use and exact Tailwind utility concept. Include the actual preset values beside named tokens. For example, map a specified border color to `border-border`, muted text to `text-muted-foreground`, and an exact radius to `rounded-[12px]` only when that value is supplied or explicitly derived. State any required semantic aliases; do not assume custom tokens or font utilities already exist. Treat utilities as blueprint annotations, not source code.

**Cognitive-load enforcement:** Allow at most one visually dominant primary action per screen, according to the architecture. Identify secondary actions that stay visible and the exact actions disclosed through `shadcn/ui DropdownMenu`, `Sheet`, tabs, or contextual expansion. Preserve essential comprehension and recovery controls. Specify the entry point and discoverability of each hidden group; not all secondary actions belong behind a menu.

**Behavioral tone:** Map anxiety, uncertainty, urgency, confidence, and completion states from the UX document to specific typography, color roles, microcopy, feedback placement, and pacing. Provide concrete copy where the meaning is known. Preserve clear error semantics even when using restrained colors; do not imply success through a soothing accent. Avoid motion or effects that compete with attention during high-stakes decisions.

**Component philosophy:** Define when to use inline editing, validation, toast feedback, dialogs, sheets, and full-page transitions based on the source journey. Specify keyboard/focus behavior and persistent feedback when it affects understanding or recovery. Match component complexity to the user's task.

**Six-principle constraints:** Give tactical rules for hierarchy of attention; proximity of related elements; alignment of content and controls; contrast for readable text, actions, and states; white space between unrelated groups; and repetition of equivalent components and behavior.

**Responsive continuity:** Specify how grouping, information order, navigation, and action priority survive narrow viewports, using concrete concepts such as `grid-cols-1`, `md:grid-cols-2`, or `min-w-0` when appropriate. Respect explicit platform constraints in the source.

### 2. Screen-by-Screen UI Blueprint

Repeat the block below for EVERY source screen. Include distinct dialogs, sheets, and interaction steps as identifiable blocks or nested subflows when they carry their own UX decisions or states. Do not combine screens in a way that loses constraints.

#### [Screen Name / Source ID]

- **Core UX Goal:** Preserve the source goal in one sentence; include the associated objects and user actions.
- **Behavioral State & UI Response:** Carry each relevant psychological insight into concrete treatment: attention order, reassurance copy, feedback, progress, interaction pace, and preset colors/typography. Explain the principle behind each treatment.
- **Layout & Proximity Rules:** Specify region order, grouping, alignment anchors, content density, responsive behavior, spacing utilities, and emphasis. Translate vague phrases such as "ample space" into concrete concepts, for example `gap-4` within a group and `space-y-8` between groups when compatible with the preset.
- **Component Inventory (Open-Source Specs):** Name the exact component or pattern, its library, its task, its placement, key behavior, and utility concepts. Prefer contextual `shadcn/ui` components and `lucide-react` icons where appropriate. Identify `Magic UI`, `Aceternity UI`, or `21st.dev` patterns only when they serve a source UX requirement and the preset. Reference patterns as design options, not as claims that packages are installed or APIs verified. Do not add decorative effects merely to include a library; specify an accessible static fallback when recommending motion.
- **Cancellation & Progressive Disclosure Enforcement:** For each source cancellation, name what is absent from the main screen, its exact destination, the trigger revealing it, and the return/dismiss behavior. Preserve the original reason and attach a design principle. Document what stays visible and why.
- **Primary Action:** Name the single dominant action, its label, exact component and emphasis utilities, availability conditions, submission feedback, and resulting branch. Classify other actions as secondary, tertiary, or contextual without making competing elements equally prominent.
- **The 5 States (Tactical Specs):** Provide separate rows or bullets for all five states below. Each must name components, content/copy, layout, utility concepts, permitted actions, feedback, and the relevant design principle. Preserve any source state distinctions within the appropriate row.

**Blank:** Distinguish first use, no results, and no available data where the architecture does. Specify a contextual illustration or icon only if useful, an explanatory heading, meaningful next action, and location. Preserve any source restrictions on the action.

**Loading:** Name the `shadcn/ui Skeleton` or equivalent pattern and describe its number, shapes, approximate dimensions, and relationship to the final layout. Use concrete concepts such as `h-5 w-40` for a text line only where appropriate. Preserve stable content and avoid layout jumps. Specify whether controls are blocked and what feedback replaces the action during submission.

**Partial:** Preserve incomplete user input, partial results, or degraded data as distinct cases when present. Specify completeness indicators, missing-field guidance, unavailable controls, retained values, and the exact completion or continuation action.

**Full:** Describe the final populated layout, information hierarchy, density behavior, and exact row/card contextual actions. Specify how long labels and extensive data remain understandable without weakening the primary goal.

**Error:** Distinguish field errors, operation failures, and unavailable data where the source does. Name inline validation, `Alert`, persistent status, or toast as appropriate; specify exact recovery controls, preserved input, and retry/dismiss/undo behavior. Provide informative text alongside color and icons. Recovery needing continued attention must not depend on a disappearing toast.

If the source labels a state not applicable, carry forward its explanation. If a required state is absent in the source, propose a minimal UI treatment and label it as a derived recommendation rather than a source requirement.

- **Recovery & Re-entry:** Map EVERY local failure, abandonment, undo, correction, or return path to a component and precise behavior. Specify whether data persists, how users resume, and what regains focus. Use an Undo toast only if the source action is reversible; do not invent rollback support.

### 3. Prototype Flow & Navigation Logic

**Transition rules:** For every decision node and branch, record source screen/state, trigger, condition, UI mechanism, destination/state, feedback, back/cancel behavior, and design-principle justification. Include success, alternative paths, failure, recovery, and re-entry. Choose between an inline change, dialog, sheet, tab, or page transition based on source context; do not default every review step to a modal.

**Shared elements:** List global navigation, repeated object representations, status labels, progress indicators, feedback surfaces, and persistent action regions that are actually implied by the architecture. Specify where each appears, changes, or is suppressed and which utilities/tokens remain consistent. Justify consistency through Repetition while allowing documented contextual differences.

**Coverage ledger:** Map each source ID to its exact section/screen/state/transition destination. Include retained scope, object relationships, behavioral insights, all states, cancellation destinations, recovery paths, and shared rules. Record deferred items as excluded by the source decision. Carry open UX risks and unresolved preset conflicts forward; do not omit them or mark them resolved without evidence.

## Final Verification

Check the finished document against the full source inventory:

- Every source screen and distinct step has a blueprint destination and all five states accounted for.
- Every decision branch, recovery path, cancellation, relocation, and psychological insight has a concrete UI treatment.
- No retained requirement is lost, deferred feature restored, or source uncertainty silently resolved.
- Every actionable directive names a design principle and explains the actual relationship.
- All six principles receive concrete treatment across the document.
- Every screen's action hierarchy respects its core goal and source audit.
- Exact preset values remain consistent across utility concepts and component/state specifications; derived values and exceptions are explicit.
- Named patterns and libraries are recommendations unless verified; no unsupported installation or API claims appear.
- The coverage ledger has no unaccounted source items.
- The output is a tactical blueprint with no implementation code.
