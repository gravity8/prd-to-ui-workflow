# Mode A — Deterministic Visual Design Spec

Use this reference only for a specified visual tool such as Stitch or Banani. Produce a visual execution specification in the four sections below. Include the named target at the beginning. Describe exact canvas, geometry, typography, layers, and visible states; do not substitute a React component tree for the visual blueprint.

## 1. Global Canvas & Grid System

Specify:

- Reference viewport width and height in pixels, and any additional viewports explicitly required by the context.
- Column count, usable content width, outer margins, gutters, baseline spacing, and permitted spacing increments.
- Coordinate origin and whether element positions are canvas-relative, parent-relative, fixed, or flow-based. Use a top-left origin unless the target requires otherwise.
- How content scrolls, how fixed/sticky regions relate to it, and exact overflow behavior.
- The global preset contract: font families, font sizes, weights, tracking, line heights, hex colors including alpha where needed, radii, border widths, and numeric shadow parameters.
- Reusable component archetypes, with source names and the structures adopted.

Check that grid arithmetic fits the canvas: margins, columns, and gutters must reconcile with the viewport width. A spacing scale is not permission to alter an explicitly supplied dimension. Label any chosen viewport or grid values missing from the source as derived specification values.

Attach a design-principle justification to each geometry or structural rule.

## 2. Screen-by-Screen Layer-by-Layer Blueprint

Repeat for EVERY approved screen, including distinct overlay or intermediate states when they have their own approved behavior.

### [Screen Name / Source ID]

**Core UX Goal:** Preserve the source intent and action priority.

**Canvas Background:** Give the exact hex value and reference viewport.

**Layer Order:** List background, navigation, content regions, feedback, and overlays in back-to-front order. Include only source-approved elements.

For every element, supply:

- **Element Name and Parent:** Identify its container and order among siblings.
- **Archetype:** Name the open-source structure and any approved adaptation.
- **Spatial Positioning:** Exact x/y, width/height or a fully specified sizing rule, padding, margins, gaps, alignment anchors, and fixed/flow/scroll behavior. For content-dependent heights, specify line height, padding, minimum/maximum bounds, and overflow instead of inventing a misleading fixed height.
- **Visual Specs:** Exact background, text and border hex values; border width; radius; shadow; font family, size, weight, tracking, line height, and alignment.
- **Interaction Appearance:** Exact active, selected, hover, keyboard-focus, disabled, or submitting appearance where applicable. Define how approved disclosures appear and how users return.
- **Design Principle Enforced:** Name the principle and explain how the decision preserves source hierarchy, grouping, attention, or consistency.

For recurring structures, define one complete shared specification and reference it by name. Include every screen-specific override; do not omit unique behavior as "same as above."

Preserve the primary action and all cancellation decisions. A relocated element must appear in its named destination, with an explicit reveal action. Avoid invisible hover-only access to essential actions.

## 3. Exact Copy & Mock Data

Provide literal headings, labels, button text, helper text, confirmations, and recovery/error messages. Preserve approved copy; label newly authored copy where the source leaves it open.

Supply 3–4 realistic synthetic records for list/table/repeated-content screens. Use the source's actual fields and relationships. Include a longer label or incomplete record only when supported by the approved content model. For a screen without repeated records, provide appropriate concrete form values or object content and explain why rows do not apply.

Use no Lorem Ipsum or unspecified "sample content." Keep fixtures consistent across related screens.

## 4. State Visualizations

Describe the appearance and behavior of all five states for every screen or distinct interaction step. Empty and Loading require detailed visual treatment; retain Partial, Full, and Error from the UI Generation Context as well.

- **Blank/Empty:** Exact position and dimensions of any approved icon/illustration, exact heading/body typography and copy, spacing, action position, and available next action.
- **Loading:** Exact number, shapes, widths, heights, radii, and positions of skeleton blocks matching the final content. Retain stable regions. Define any skeleton animation numerically and its reduced-motion alternative; do not add an animation if the preset forbids it.
- **Partial:** Exact placement of incomplete-content indicators, missing-field guidance, remaining data, and permitted continuation actions.
- **Full:** Refer to the populated layer blueprint and fixtures; specify any visible density, truncation, wrapping, or overflow behavior.
- **Error:** Exact placement, icon dimensions if used, typography, status colors, recovery copy/control, and preserved input or data. Distinguish local errors from screen-blocking failures where the source does.

For each state, specify the trigger, transition destination, and relevant design principle. If the target produces static screens, name each state variant as a separate frame and describe the intended transition without claiming the tool can implement it.
