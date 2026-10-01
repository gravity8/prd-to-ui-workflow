# Mode B — Deterministic Code Architecture Spec

Use this reference only for a specified code tool such as v0, Lovable, or Bolt. Produce a specification in the four sections below, beginning with the target name. Short component-tree annotations, conditional expressions, and mock-data JSON are appropriate; do not build or output an entire application.

## 1. Global Tech Stack & Component Strategy

Use the requested baseline: **React, Tailwind CSS, shadcn/ui, lucide-react**. Respect an explicit user override. Name additional approved archetypes such as Magic UI or a specific 21st.dev pattern only where they support the UI context.

Specify:

- Shared layout/component archetypes, their responsibilities, and reuse boundaries.
- Exact preset-to-Tailwind mappings: hex arbitrary values, font-size/line-height values, weight, tracking, spacing, borders, radius, shadows, and motion.
- Font-family and semantic token definitions required for utilities such as `font-heading`, `border-border`, or `text-muted-foreground`; do not assume these custom aliases exist.
- Whether values should be expressed as arbitrary-value classes or semantic aliases, with a complete value table for the chosen approach.
- Exact class strings for shared primary/secondary actions, focus, disabled, validation, and feedback states.

For example, a supplied color may map to `bg-[#FDF7F7]`; do not reuse this example color unless it is in the preset. If the environment specifies a Tailwind version, keep any configuration guidance compatible with it. If the version is unknown, use concrete arbitrary-value class concepts and state the alias definitions needed instead of asserting an unverified configuration format.

Map every structural choice to a named design principle with a concrete reason. Archetypes are design sources, not permission to claim that dependencies are installed.

## 2. Screen-by-Screen Component Tree & Tailwind Specs

Repeat for EVERY approved screen and identify distinct dialogs, sheets, or intermediate steps with their own behavior.

### [Screen Name / Source ID]

**Core UX Goal:** One sentence preserving the source goal.

**Component Hierarchy (DOM Structure):** Give an indented tree from the shared shell through all meaningful content, actions, feedback, and disclosures. For each node, specify:

- React component name or semantic DOM element.
- Library component/archetype, or the named archetype composed by a project-local wrapper.
- Exact Tailwind class string for layout and appearance, including responsive variants where required.
- Data/content binding and any visibility or enabled-state condition.
- Named design principle and the user-facing reason.

Tree notation such as `<Layout>` and `<main>` is a hierarchy annotation, not a complete JSX implementation. Do not omit component names, classes, or conditions behind vague instructions such as "style consistently."

Specify width/height ownership, content wrapping, overflow, and alignment. Avoid contradictory shell geometry, such as adding a sidebar offset to a main region already positioned by a grid. Preserve approved primary actions and progressive disclosure: define exact menu/sheet/dialog contents, reveal action, close behavior, and returned focus.

**Design Principle Enforcement:** Explain the most consequential combinations of class values and structure for this screen. Each tree node must still carry its own relevant mapping; this summary does not replace it.

## 3. The 5 States Logic — Required

Define the state variables and data shapes before stating rendering conditions. Supply exact conditional expressions or a mutually exclusive decision table with exact predicates, component names, and class strings. Cover all five states, not just Loading and Empty.

Specify precedence so simultaneous flags cannot render conflicting states. Distinguish initial loading from background refresh with already available data when the source requires it. Empty must mean a successful resolved response with no content, not merely `data` being undefined.

For each state, give its trigger, predicate, rendered component, exact styling/content, allowed actions, transition destination, and design-principle justification:

- **Loading:** Use a named skeleton component with exact class strings for all placeholder shapes, matched to final rows/cards/content. Never use spinners. Define what remains visible and which controls are disabled during submission or refresh.
- **Blank/Empty:** Define `EmptyState` or an equivalent named composition, including exact icon size, headings, copy, primary action, and classes. Ensure the empty predicate cannot mask an error.
- **Partial:** Define incomplete input or partially available content from the source, with exact predicates, completeness guidance, validation, and continuation rules. Do not equate fewer rows with partial data unless the approved model does.
- **Full:** Define the successful populated condition, bindings to the mock-data structure, row/card hierarchy, contextual actions, and density/overflow behavior.
- **Error:** Define field-level and operation-level errors where applicable, retained values/data, inline or persistent feedback, exact classes, and correction/retry/return actions. Do not claim undo or persistence capabilities absent from the approved context.

If a source state is not applicable, retain the explanation. For a missing state, label the recommended definition as derived rather than an approved upstream requirement. Include keyboard focus and status announcement behavior where necessary for users to understand or recover from the state.

## 4. Mock Data & Interactions

Provide realistic synthetic JSON or array fixtures with stable IDs, exact field names and types, and relationships consistent with the approved objects. Include 3–4 records where the interface renders repeated content, so Full can be demonstrated immediately. For form/detail screens, provide corresponding field values or an object fixture instead.

Include fixtures or state flags needed to demonstrate the other applicable states without inventing product features. The prototype must not require a live service merely to display these fixtures.

Map EVERY approved action and decision branch to:

- Trigger and precondition.
- Local state update, navigation target, or disclosure change.
- Submission/loading and success/failure feedback.
- Recovery, preserved input, back/cancel behavior, and returned focus where applicable.
- Exact component, classes, and principle justification.

Specify micro-interactions only where appropriate to the preset and source intent. Give exact properties, duration, easing, hover/focus behavior, and reduced-motion alternative; avoid adding decorative animation as a substitute for behavioral feedback.

Mark mock interactions as simulated. Do not invent endpoints, persistence, authentication, or backend architecture to make a visual prototype look functional.
