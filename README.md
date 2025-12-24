# Assistant Estimation Pack

A comprehensive toolkit for generating consistent feature breakdowns, estimates, and user stories for product requirements. Outputs follow Scrum/Kanban-friendly formats with task-level granularity suitable for sprint planning and backlog management.

## Overview

This pack provides:

- **Guidelines** for consistent estimation and breakdown methodologies
- **Templates** ready to fill for feature breakdowns, estimations, and user stories
- **Prompts** including system prompts and sample inputs/outputs
- **Best practices** for agile estimation and story writing

## Project Structure

```text
assistant-estimation/
├── guidelines/          # Methodology and rules
│   ├── breakdown-rules.md      # How to decompose features into tasks
│   ├── estimation-method.md    # How to size work and apply buffers
│   └── story-format.md         # User story and AC guidance
├── templates/           # Ready-to-fill templates
│   ├── feature-breakdown-template.md
│   ├── estimation-template.md
│   └── story-template.md
├── prompts/             # AI assistant prompts and examples
│   ├── system-prompt.md
│   ├── sample-inputs/   # Example requirements
│   └── sample-outputs/  # Example outputs
└── README.md           # This file
```

## Quick Start

1. **Read the guidelines** in `guidelines/` to understand the methodology
2. **Review sample inputs** in `prompts/sample-inputs/` to see example requirements
3. **Check sample outputs** in `prompts/sample-outputs/` to see expected formats
4. **Use the system prompt** (`prompts/system-prompt.md`) with your AI assistant
5. **Fill templates** from `templates/` with your breakdowns and estimates

For detailed step-by-step instructions, see [USAGE.md](USAGE.md).

## Key Concepts

### Estimation Units

- **Person-Day (PD)**: 6 focused hours of work
- **Confidence Levels**: High (≥70% knowns), Medium (some unknowns), Low (many unknowns)
- **Risk Buffers**: Low +10%, Medium +20%, High +35%

### Breakdown Hierarchy

- **Feature**: User-facing capability or major service area
- **Epic/Story**: Coherent slice delivering value; sprint-sized
- **Task**: Single-discipline unit (Mobile, FE, BE, QA, Ops) ideally ≤2 PD

### Output Formats

All outputs use concise, action-oriented language with tables for clarity. See `prompts/sample-outputs/` for complete examples.

## Usage Workflow

1. **Input**: Provide product requirements (see `prompts/sample-inputs/` for format)
2. **Breakdown**: Decompose features → epics → stories → tasks using `templates/feature-breakdown-template.md`
3. **Estimation**: Size tasks and apply buffers using `templates/estimation-template.md`
4. **Stories**: Write user stories with AC using `templates/story-template.md`
5. **Review**: Capture assumptions, dependencies, risks, and critical path

## Best Practices

- Always clarify scope and assumptions before estimating
- Include cross-cutting concerns: security, observability, QA, DevOps
- Document dependencies and blockers clearly
- Apply risk buffers based on confidence levels
- Keep tasks independent and testable where possible
- Follow Definition of Ready (DoR) and Definition of Done (DoD) criteria

## Examples

See `prompts/sample-inputs/payment-app-requirement.md` for a complete example requirement, and `prompts/sample-outputs/` for corresponding breakdowns, estimates, and stories.
