# Mode A — Deterministic Visual Design Spec

Use this reference only for a specified visual tool such as Stitch or Banani. Produce a rigid, parser-ready visual execution specification in the five sections below. Include the named target at the beginning. Describe exact canvas, geometry, typography, color allocation, layers, and visible states; do not substitute a React component tree for the visual blueprint. The downstream tool must not need to infer placement, component structure, or color semantics.

## 1. Global Canvas & Grid System

Specify:

- Reference viewport width and height in pixels, and any additional viewports explicitly required by the context.
- Column count, usable content width, outer margins, gutters, baseline spacing, and permitted spacing increments. Default a missing baseline to an 8px system and require all derived margins, padding, and gaps to be multiples of 8. Preserve an explicit preset spacing value even when it is off-grid, and flag it as a preset exception rather than silently rounding it.
- Coordinate origin and whether element positions are canvas-relative, parent-relative, fixed, or flow-based. Use a top-left origin unless the target requires otherwise.
- How content scrolls, how fixed/sticky regions relate to it, and exact overflow behavior.
- The global preset contract: font families, font sizes, weights, tracking, line heights, hex colors including alpha where needed, radii, border widths, and numeric shadow parameters.
- Reusable component archetypes, with source names and the structures adopted.

Check that grid arithmetic fits the canvas: margins, columns, and gutters must reconcile with the viewport width. A spacing scale is not permission to alter an explicitly supplied dimension. Label any chosen viewport or grid values missing from the source as derived specification values.

Attach a design-principle justification to each geometry or structural rule.

## 2. Strict Color Principles & Application

Build an element-level color contract before specifying screens. Use actual preset values beside every semantic role; never substitute example colors from this reference.

### 60–30–10 hierarchy and balance

- **Approximately 60% neutral backgrounds:** page background and surface colors occupy most visible area and preserve White Space.
- **Approximately 30% structural neutrals:** border, muted text, table grid, secondary icon, disabled, and skeleton colors provide structure without noise.
- **No more than 10% brand accent/action:** reserve the brand accent for the one primary CTA, active navigation or selection, keyboard focus, links where the preset assigns them, and source-approved critical highlights. Never use the accent as the background of a large page region or ordinary card.
- Explain any source-required exception, including semantic warning/error regions, without recasting it as brand accent usage.

### Contrast and accessibility

- Define every permitted foreground/background pair and state whether it is for body text, large text, iconography, or decoration. Body text must meet at least 4.5:1 contrast; large text at least 3:1; interactive boundaries and focus indicators at least 3:1 against adjacent colors.
- Never describe a color in isolation. State its exact hex/alpha, paired background, semantic role, and permitted elements.
- Specify non-color cues for success, warning, error, selection, disabled, and focus states.

### Semantic consistency

- Map brand accent, secondary accent, success, warning, destructive, primary text, muted text, border, background, and surface to one stable meaning each.
- Destructive actions use the destructive semantic color, never the brand accent. Success and positive states use the success role, not the action role, unless the preset explicitly makes them the same; document that collision.
- Muted text is limited to inactive states, placeholders, secondary descriptions, and metadata where contrast remains sufficient.

### Grouping via tints

- When the preset permits tinting, use a 5–10% alpha of the brand accent or the preset's explicit soft token to group related content without a harsh border. State the computed or supplied color and the exact container where it applies.
- Do not invent a tint when the preset forbids translucency or supplies a distinct grouping token.

For every screen, include a compact color-allocation check naming the large neutral surfaces, structural neutral elements, accent elements, and semantic-state elements. Treat 60–30–10 as an approximate visual-area discipline, not an image-pixel audit.

## 3. Screen-by-Screen Layer-by-Layer Blueprint

Repeat for EVERY approved screen, including distinct overlay or intermediate states when they have their own approved behavior.

### [Screen Name / Source ID]

**Core UX Goal:** Preserve the source intent and action priority.

**Canvas Background:** Give the exact hex value and reference viewport.

**Visual Hierarchy / Eye Path:** State the exact first, second, and third visual fixation and whether the screen uses an F-pattern, Z-pattern, list-detail scan, or another source-supported reading pattern. Tie each fixation to position, scale, contrast, and the dominant action.

**Layer Order:** List background, navigation, content regions, feedback, and overlays in back-to-front order. Include only source-approved elements.

For every element, supply:

- **Element Name and Parent:** Identify its container and order among siblings.
- **Archetype:** Name the open-source structure and any approved adaptation. For `shadcn/ui`, Magic UI, or `21st.dev`, describe the adopted anatomy in order—container, header, body, repeated item, controls, feedback, and overlay—rather than only naming a pattern. Never imply an export or package is installed.
- **Spatial Positioning:** Exact canvas-relative or parent-relative x/y, width/height or a fully specified sizing rule, padding, margins, gaps, alignment anchors, and fixed/flow/scroll behavior. State coordinate context for every element. For content-dependent heights, specify line height, padding, minimum/maximum bounds, and overflow instead of inventing a misleading fixed height. Derived coordinates and gaps follow the 8px baseline; preset exceptions remain exact and labelled.
- **Visual Specs:** Exact background, text and border hex values; permitted foreground/background pair; border width; radius; shadow; font family, size, weight, tracking, line height, and alignment. State whether the element belongs to the 60% neutral, 30% structural, 10% accent, or semantic-state allocation.
- **Interaction Appearance:** Exact active, selected, hover, keyboard-focus, disabled, or submitting appearance where applicable. Define how approved disclosures appear and how users return.
- **Design Principle Enforced:** Name the principle and explain how the decision preserves source hierarchy, grouping, attention, or consistency.

For recurring structures, define one complete shared specification and reference it by name. Include every screen-specific override; do not omit unique behavior as "same as above."

Preserve the primary action and all cancellation decisions. A relocated element must appear in its named destination, with an explicit reveal action. Avoid invisible hover-only access to essential actions.

Close every screen block with:

- **Color Allocation Check:** List the exact elements occupying neutral background/surface, structural neutral, accent/action, and semantic-state roles; confirm the accent remains visually subordinate to the content and dominant action.
- **Principle Ledger:** For every major spatial and color decision, name Hierarchy, Proximity, Alignment, Contrast, White Space, or Repetition and explain the specific user benefit. Do not rely on a document-wide rationale.

## 4. Exact Copy & Mock Data

Provide literal headings, labels, button text, helper text, confirmations, and recovery/error messages. Preserve approved copy; label newly authored copy where the source leaves it open.

Supply 3–4 realistic synthetic records for list/table/repeated-content screens. Use the source's actual fields and relationships. Include a longer label or incomplete record only when supported by the approved content model. For a screen without repeated records, provide appropriate concrete form values or object content and explain why rows do not apply. For each literal string or record field, specify its parent element, position within that parent, typography, color pair, wrapping/truncation rule, and alignment. Coordinates may reference the screen's already-defined parent-relative layout instead of duplicating absolute canvas coordinates.

Use no Lorem Ipsum or unspecified "sample content." Keep fixtures consistent across related screens.

## 5. State Visualizations

Describe the appearance and behavior of all five states for every screen or distinct interaction step. Empty and Loading require detailed visual treatment; retain Partial, Full, and Error from the UI Generation Context as well.

- **Blank/Empty:** Exact position and dimensions of any approved icon/illustration, exact heading/body typography and copy, spacing, action position, and available next action. Define the first/second/third eye path and color allocation for the empty state.
- **Loading:** Exact number, shapes, widths, heights, radii, and positions of skeleton blocks matching the final content. Retain stable regions. Define any skeleton animation numerically and its reduced-motion alternative; do not add an animation if the preset forbids it.
- **Partial:** Exact placement of incomplete-content indicators, missing-field guidance, remaining data, and permitted continuation actions.
- **Full:** Refer to the populated layer blueprint and fixtures; specify any visible density, truncation, wrapping, or overflow behavior.
- **Error:** Exact placement, icon dimensions if used, typography, status colors, recovery copy/control, and preserved input or data. Distinguish local errors from screen-blocking failures where the source does.

For each state, specify the trigger, transition destination, and relevant design principle. If the target produces static screens, name each state variant as a separate frame and describe the intended transition without claiming the tool can implement it.

## Parser-Ready Formatting Rules

- Use the five numbered sections above in order and one consistently structured screen block per approved screen.
- Prefer tables or repeated labelled fields where they keep element attributes unambiguous; do not compress required attributes into prose that changes shape from screen to screen.
- Use exact integers for coordinates and dimensions where the layout is fixed. When a dimension is content-driven, use an explicit rule such as `height: auto; min 72px; max 116px; overflow: two-line clamp` rather than an estimate.
- Distinguish every supplied preset value from a **Derived specification value** and every source requirement from a derived visual treatment.
- Do not include rationale or commentary that could be mistaken for UI copy inside a downstream prompt block. Keep principle justifications in their labelled fields.
