---
name: technical-design-document
description: Creates a detailed technical design document from a product opportunity through collaborative workshopping. Use this when the user wants to create a technical spec, design document, or needs to plan a new feature or project through an interactive process with discovery, alternatives exploration, and iterative feedback before finalizing.
---

# Technical Design Workshop

Guide users through creating a comprehensive technical design document from a product one-pager through an interactive, workshop-style conversation.

## Workshop Flow

Follow these phases sequentially, adapting based on project context:

### Phase 1: Read Product One-Pager

**Accept input in any format:**
- Full product document
- Brief description (1-2 sentences)
- Key problem/solution statements

**Clarification protocol:**
- Assume provided context is complete
- Only ask clarifying questions if critical "what" or "why" information is missing
- Keep questions minimal and focused

### Phase 2: Discovery

**Scan the project environment:**

```bash
# Check current directory structure
ls -la
# Read key documentation files
cat README.md agents.md claude.md 2>/dev/null
```

**Present findings:**
- Summarize existing codebase/files
- Note if starting from scratch
- Highlight relevant documentation found

**Ask user:** "Is there anything important I'm missing or should know before we proceed?"

Wait for confirmation before advancing.

### Phase 3: Scoping (Critical Phase)

Work collaboratively to define boundaries. This is the most important phase.

**Define In-Scope features:**
- Identify 3-5 core features to include
- Explain why each is essential
- Consider existing codebase elements
- Prefer iteration over rewrites

**Define Out-of-Scope items:**
- Be explicit about exclusions
- Explain deferral rationale
- Maintain focus on core functionality

**Important constraints:**
- Don't sequence implementation (that's for later)
- Write for AI agent audience (concise, technical)
- Focus on WHAT to build, not HOW
- No code, READMEs, or artifacts yet

**Interaction style:**
- Ask ONE question at a time
- Use multiple-choice format (2-4 options)
- Present trade-offs clearly
- Invite feedback on alternatives

**Example question:**
"Which features are most critical for V1?
A) User authentication + basic CRUD (faster launch)
B) Authentication + CRUD + search (more complete)
C) Just CRUD operations (minimal viable)
D) Something else - what would you prioritize?"

### Phase 4: Technology Choices

**For existing projects:**
- Use current technology stack
- Respect existing patterns
- Avoid unnecessary rewrites

**For new projects, prefer:**
- Frontend: React, TypeScript, Tailwind CSS
- Backend: Node.js and/or Python
- Minimize dependencies
- Apply AI agent best practices

**When multiple options exist:**
- Present 2-3 alternatives maximum
- Explain trade-offs (performance, complexity, maintainability)
- Use multiple-choice format

**Example:**
"Database approach for this project?
A) PostgreSQL (relational, robust, slightly more setup)
B) SQLite (simple, file-based, perfect for small scale)
C) MongoDB (flexible schema, good for rapid iteration)"

### Phase 5: Write Technical Design Document

Create a structured document with these sections:

#### Required Sections

**1. Overview**
- What we're building (1-2 sentences)
- Why we're building it (1-2 sentences)
- Success criteria

**2. Scope**
- In-scope features (bulleted list with brief rationale)
- Out-of-scope items (what we're not building)

**3. Architecture**
- High-level architecture diagram (ASCII art)
- Key components and their responsibilities
- Data flows between components
- Integration points (if extending existing code)

**4. Technology Stack**
- Frontend technologies and rationale
- Backend technologies and rationale
- Key dependencies
- Infrastructure considerations

**5. Data Model** (if applicable)
- Core entities
- Relationships
- Key attributes
- Storage decisions

**6. API/Interface Design** (if applicable)
- Key endpoints or interfaces
- Request/response patterns
- Authentication/authorization approach

**7. Implementation Considerations**
- Key technical challenges
- Assumptions and dependencies
- Security considerations
- Performance considerations

#### ASCII Architecture Diagram Example

```
┌─────────────┐         ┌──────────────┐
│   Frontend  │────────▶│   API Layer  │
│  (React)    │◀────────│   (Node.js)  │
└─────────────┘         └──────┬───────┘
                               │
                        ┌──────▼───────┐
                        │   Database   │
                        │ (PostgreSQL) │
                        └──────────────┘
```

#### Writing Style

**Concise and focused:**
- Write for an AI agent with technical knowledge
- Minimal explanation of well-known concepts
- Clear structure with logical sections
- No unnecessary verbosity

**What to include:**
- Component purposes and interactions
- Data flows and state management
- Integration boundaries
- Technical decisions and rationale

**What to omit:**
- Detailed implementation steps
- Code snippets (unless illustrating a pattern)
- Overly detailed explanations of standard technologies
- Project management details

## When to Stop the Workshop

You have sufficient information when you can clearly answer:

1. ✓ What are we building? (feature list is clear)
2. ✓ What are we NOT building? (exclusions are explicit)
3. ✓ What technology will we use? (stack decisions made)
4. ✓ How do components interact? (architecture is clear)

Stop asking questions once these are answered. Write the technical design document.

## Interaction Principles

**Be collaborative, not interrogative:**
- You're facilitating a workshop, not conducting an interview
- Invite discussion on alternatives
- Trust user's judgment on scope
- Make technical decisions explicit

**Efficiency over completeness:**
- Don't over-engineer the conversation
- Focus on decisions that matter
- Skip obvious or low-impact choices
- Keep scope manageable

**AI-First documentation:**
- Remember your audience is an AI implementing this
- No need to explain basics
- Focus on the "what" not the "how"
- Provide enough context for autonomous implementation

## Example Workshop Flow

```
User: "I want to build a note-taking app with AI-powered search"

Claude: "I'll help you create a technical spec for that. Let me first 
check what's in your current project folder..."

[Runs discovery commands]

Claude: "I see you have an empty project folder. This will be a fresh 
start. Before we scope this out, is there anything about your existing 
infrastructure or constraints I should know?"

User: "No, starting fresh"

Claude: "Great. For the AI-powered note-taking app, which features are 
most critical for the first version?

A) Basic notes + AI semantic search (core functionality)
B) Notes + AI search + tagging/folders (more organized)
C) Notes + AI search + collaboration (multi-user focus)
D) Something else - what's your priority?"

[Continues workshop through phases...]
```
