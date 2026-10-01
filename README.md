# PRD-to-UI Workflow

A reusable Codex skill workflow that turns a Product Requirements Document into UX architecture, a UI blueprint, and a specification for an AI design tool.

Invoke one skill to run all three stages:

```text
$prd-to-ui-workflow

PRD: [paste the document or identify the attached file]
Design Preset: [provide typography, palette, shape, spacing, and other design rules]
Target Tool: [Stitch, Banani, v0, Lovable, or Bolt]
```

The workflow passes complete outputs between stages, asks for missing inputs, and preserves feature scope, decision branches, recovery paths, five data states, and design-principle justifications.

## Included skills

| Skill | Role |
| --- | --- |
| [prd-to-ui-workflow](prd-to-ui-workflow/SKILL.md) | Orchestrates the complete workflow and checks handoffs. |
| [zero-designer-ux](zero-designer-ux/SKILL.md) | Audits JTBD features, models user objects, maps behavioral flows, and evaluates cognitive load. |
| [ux-to-ui-blueprint](ux-to-ui-blueprint/SKILL.md) | Applies the design preset to produce screen-by-screen UI directives. |
| [ui-tool-spec](ui-tool-spec/SKILL.md) | Produces exact visual or code architecture specifications for the selected tool. |

## Installation

Install all four skill folders into your Codex skills directory, typically `~/.codex/skills/`, or into `$CODEX_HOME/skills` if configured. Keep the folders as siblings: the orchestrator loads the other skills through relative links.

You can also ask Codex to install all four skills from this repository:

```text
Install prd-to-ui-workflow, zero-designer-ux, ux-to-ui-blueprint, and ui-tool-spec
from the GitHub repository gravity8/prd-to-ui-workflow.
```

Each skill includes its own `SKILL.md` and UI metadata. The tool specification skill also includes separate references for visual and code modes. The skills can be invoked individually when only one stage is needed.

## Outputs

1. `01-ux-architecture.md`
2. `02-ui-generation-context.md`
3. `03-tool-specification.md`

Visual mode describes canvas geometry, layers, exact copy, mock data, and state visualizations. Code mode describes React component hierarchy, Tailwind specifications, state rendering conditions, and mock interactions.

The workflow produces planning and handoff documents. It does not build an application or submit prompts to external tools. Tool-specific code annotations belong to the final code architecture specification.

The orchestrator can resume after missing inputs are supplied and refresh the affected downstream stages when the PRD, preset, or target changes.
