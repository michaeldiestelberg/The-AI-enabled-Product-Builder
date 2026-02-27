# UX IA Review

`ux-ia-review` is an AI skill for reviewing UI screenshots with a strict focus on:

- usability
- information architecture

It does **not** focus on visual polish (colors, typography, branding, aesthetics), except where visual issues directly block usability.

## What it produces

When given a screenshot, this skill outputs:

1. What it found in the current structure and flow
2. What should change (current state -> proposed change -> rationale -> priority)
3. An optional IA restructuring direction
4. A copy/paste-ready prompt for a coding agent that explains **what** to change, not **how** to implement it

## Typical use cases

- Reviewing a page or screen for navigation clarity
- Improving task flow and discoverability
- Reorganizing confusing layout/grouping and labels
- Converting UX/IA findings into implementation-ready direction for another coding agent
