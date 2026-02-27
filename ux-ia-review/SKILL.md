---
name: ux-ia-review
description: Review a provided UI screenshot for usability and information architecture quality, then propose concrete structural changes with rationale and generate a copy/paste prompt for a coding agent. Use when the user asks for UX review, IA review, layout structure critique, navigation clarity feedback, or task-flow improvement based on a screenshot or mockup.
---

# UX IA Screenshot Review

Review one or more screenshots to diagnose usability and information architecture issues, then convert findings into actionable structural changes and a coding-agent-ready prompt.

## Scope Rules

- Focus on usability and information architecture only.
- Analyze hierarchy, grouping, labeling, navigation, task flow, discoverability, and cognitive load.
- Avoid visual-style critique (colors, typography, icon style, branding, aesthetics) unless it directly blocks usability.
- Avoid technical implementation instructions (frameworks, CSS, component APIs, code-level detail).

## Required Inputs

- Use at least one screenshot provided by the user.
- Use optional context when available: user type, primary task, device type, and product goal.
- State explicit assumptions when context is missing instead of blocking progress.

## Workflow

### 1. Map the Current Structure

- Identify major regions: global navigation, local navigation, page header, content areas, sidebars, utilities, and calls to action.
- Describe the apparent primary task and secondary tasks supported by the screen.
- Note the reading/order path implied by layout and emphasis.

### 2. Evaluate Information Architecture

- Check grouping and chunking of related information.
- Check labeling clarity and whether terms match user intent.
- Check findability of key actions and key information.
- Check hierarchy depth and whether users can orient themselves quickly.

### 3. Evaluate Usability

- Check whether the next action is obvious at each stage.
- Check friction points, ambiguity, duplicated decisions, and dead ends.
- Check whether the interface likely increases cognitive load unnecessarily.
- Check whether navigation and content structure support the main workflow.

### 4. Define Change Proposals

For every meaningful issue, provide:
- What exists now (current structure/behavior).
- What should change (target structure/behavior).
- Why the change improves usability or IA.
- Priority (`High`, `Medium`, `Low`) based on impact on key task completion.

### 5. Generate Coding-Agent Prompt

Produce a final prompt that tells a specialized coding agent what to change, not how to code it.

- Include explicit goals and constraints.
- List required UX/IA changes in priority order.
- Include rationale to preserve intent.
- Include acceptance criteria phrased in UX/IA outcomes.
- Exclude technical implementation details.

## Output Format

Always return sections in this order:

### 1) What I Found

- Summarize the current screen structure in 4-8 bullets.
- State the primary task the user appears to be trying to complete.
- State assumptions if context is missing.

### 2) What Needs To Change

Use a table with these columns:
- `Issue`
- `Current State`
- `Proposed Change`
- `Why This Improves UX/IA`
- `Priority`

### 3) Structural Direction (Optional)

- Provide a compact proposed IA outline when re-organization is substantial.
- Use simple bullets or numbered lists for navigation/content structure.

### 4) Copy/Paste Prompt For Coding Agent

Return a fenced `text` block with this shape:

```text
You are improving the UX and information architecture of an existing interface.

Objective:
- [Outcome-focused objective]

Constraints:
- Focus on usability and information architecture only.
- Do not spend effort on visual styling changes unless required for usability.
- Implement WHAT should change; choose HOW to implement.

Required changes (in priority order):
1. [Change request]
2. [Change request]
3. [Change request]

Rationale to preserve:
- [Key UX/IA reasoning]

Acceptance criteria:
- [Observable UX/IA outcome]
- [Observable UX/IA outcome]
- [Observable UX/IA outcome]
```

## Quality Bar

- Tie every recommendation to evidence visible in the screenshot.
- Translate diagnosis into concrete structural change requests.
- Keep findings specific and actionable; avoid generic UX advice.
- Keep language implementation-agnostic for the final coding-agent prompt.
