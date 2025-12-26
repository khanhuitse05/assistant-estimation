# Assistant Estimation Pack

A comprehensive toolkit for generating consistent feature breakdowns, estimates, and user stories for product requirements. Outputs follow Scrum/Kanban-friendly formats with task-level granularity suitable for sprint planning and backlog management.

## Overview

This pack provides:

- **Guidelines** for consistent estimation and breakdown methodologies
- **System prompt** for configuring AI assistants to generate consistent estimation outputs
- **Sample outputs** demonstrating expected formats and structure
- **Best practices** for agile estimation and story writing

## Project Structure

```text
assistant-estimation/
├── guidelines-estimation.md   # Methodology and rules (breakdown, estimation, story format)
├── system-prompt.md           # AI assistant system prompt for estimation tasks
├── sample-outputs.md          # Example estimation outputs and formats
└── README.md                  # This file
```

## Quick Start

1. **Read the guidelines** (`guidelines-estimation.md`) to understand the methodology for breakdown, estimation, and story writing
2. **Review sample outputs** (`sample-outputs.md`) to see expected estimation formats and examples
3. **Use the system prompt** (`system-prompt.md`) with your AI assistant for consistent estimation outputs
4. **Follow the workflow** outlined in the system prompt: wait for requirements → clarify scope → breakdown → estimate → write stories

## Key Concepts

### Estimation Units

- **Person-Day (PD)**: 8 hours per day of work
- **Platform/Type**: Mobile, Web, API, AI, Design, Admin ...
- **Task Complexity**: Low, Medium, High, Very High

### Breakdown Hierarchy

- **Feature/Module**: User-facing capability or major service area
- **Story**: Coherent slice delivering value; sprint-sized
- **Task**: Single-discipline unit (Mobile, FE, BE, QA, Ops) ideally ≤2 PD

### Output Formats

All outputs use concise, action-oriented language with hierarchical tables for clarity. See `sample-outputs.md` for complete examples.

## Usage Workflow

1. **Input**: Provide product requirements to your AI assistant
2. **System Prompt**: Use `system-prompt.md` to configure your AI assistant for estimation tasks
3. **Breakdown**: Decompose features → epics → stories → tasks following `guidelines-estimation.md`
4. **Estimation**: Size tasks and apply buffers using the hierarchical table format (see `sample-outputs.md`)
5. **Stories**: Write user stories with AC following the format in `guidelines-estimation.md`
6. **Review**: Capture assumptions, dependencies, risks, and critical path

## Best Practices

- Always clarify scope and assumptions before estimating
- Include cross-cutting concerns: security, observability, QA, DevOps
- Document dependencies and blockers clearly
- Apply risk buffers based on confidence levels
- Keep tasks independent and testable where possible
- Follow Definition of Ready (DoR) and Definition of Done (DoD) criteria

## Examples

See `sample-outputs.md` for a complete example estimation output including feature breakdown, effort estimates, and user stories for a mobile payment application.
