---
name: product-requirements-document
description: Creates a detailed product requirements document (PRD) from a product idea through collaborative workshopping. Use this when the user wants to define product requirements, user stories, and business rationale through an interactive process with discovery, alternatives exploration, and iterative feedback before finalizing.
---

# Product Requirements Workshop

Guide users through creating a comprehensive product requirements document from an initial product idea through an interactive, workshop-style conversation.

## Workshop Flow

Follow these phases sequentially, adapting based on project context:

### Phase 1: Capture Product Vision

**Accept input in any format:**
- Full product concept
- Brief description (1-2 sentences)
- Problem statement or opportunity
- Existing one-pager or pitch

**Clarification protocol:**
- Assume provided context is complete
- Only ask clarifying questions if critical problem/user/value information is missing
- Keep questions minimal and focused

### Phase 2: Discovery

**Scan the project environment:**

```bash
# Check current directory structure
ls -la
# Read key documentation files
cat README.md one-pager.md product-brief.md 2>/dev/null
# Check for design artifacts
ls -la designs/ mockups/ figma/ 2>/dev/null
```

**Present findings:**
- Summarize existing documentation
- Note any design artifacts found
- Highlight relevant context

**Ask user:** "Is there anything important I'm missing—existing research, competitor analysis, or constraints I should know about?"

Wait for confirmation before advancing.

### Phase 3: Audience & Value Definition (Critical Phase)

Work collaboratively to define who benefits and why. This shapes everything else.

**Define Target Users:**
- Identify 1-3 primary user personas
- Clarify their core pain points
- Understand their current workarounds

**Define Value Proposition:**
- What specific problem does this solve?
- Why will users choose this over alternatives?
- What's the measurable outcome for users?

**Interaction style:**
- Ask ONE question at a time
- Use multiple-choice format (2-4 options)
- Present trade-offs clearly
- Invite feedback on alternatives

**Example question:**
"Who is the primary user for this feature?
A) End consumers (direct value, longer feedback loops)
B) Business users/admins (power features, training needs)
C) Developers/technical users (API-first, documentation heavy)
D) Multiple personas—which should we prioritize?"

### Phase 4: User Story Development (Critical Phase)

Collaboratively build the user story backlog. This is where requirements take shape.

**Story creation approach:**
- Group stories by user goal or workflow
- Use standard format: "As a [user], I want [action] so that [outcome]"
- Include acceptance criteria for each story
- Prioritize ruthlessly

**Story prioritization:**
- Must-have (blocks launch without it)
- Should-have (significant value, but not blocking)
- Nice-to-have (enhances experience, can defer)

**Interaction style:**
- Present draft stories for validation
- Ask about edge cases and exceptions
- Clarify acceptance criteria together
- Challenge scope creep gently

**Example question:**
"For the search functionality, which scenario is most critical?
A) Basic keyword search (fast to build, limited results)
B) Filtered search with categories (more useful, moderate complexity)
C) AI-powered semantic search (best results, significant effort)
D) Something else—what's the core search need?"

### Phase 5: Business Rationale

Work with user to articulate business justification.

**Customer value paragraph:**
- What problem does this solve for customers?
- How does it improve their workflow/outcome?
- What's the competitive advantage?

**Business value paragraph:**
- How does this drive revenue/retention/expansion?
- What strategic goal does it support?
- What's the cost of not building this?

**Interaction style:**
- Draft initial rationale based on earlier discussion
- Ask user to validate or refine
- Keep it concrete and measurable where possible

**Example question:**
"Which business driver is most important for this feature?
A) New customer acquisition (market expansion)
B) Existing customer retention (reduce churn)
C) Revenue expansion (upsell/cross-sell)
D) Operational efficiency (reduce support load)
E) Strategic positioning (competitive differentiation)"

### Phase 6: UX & Design Context (Optional)

Gather design requirements and references.

**If design artifacts exist:**
- Reference specific files/links found in discovery
- Note which user stories they cover
- Identify gaps needing design work

**If no artifacts exist:**
- Document key interaction patterns needed
- Note critical UX considerations
- Flag areas requiring design attention

**Design documentation options:**
- Figma links or frame references
- Uploaded mockup files
- Wireframe descriptions
- Interaction flow descriptions

**Example question:**
"How should we handle the design documentation?
A) Reference existing Figma files (I found some in /designs)
B) Describe key interactions in text (design comes later)
C) Include uploaded mockup images
D) Skip for now—design follows requirements"

### Phase 7: Write Product Requirements Document

Create a structured document with these sections:

#### Required Sections

**1. Executive Summary**
- Product/feature name
- One-paragraph description of what we're building
- Target users (1-2 sentences)
- Key success metrics (2-3 measurable outcomes)
- Timeline/release target (if known)

**2. Business Rationale**

*Customer Value*
One paragraph explaining:
- The specific problem being solved
- How this improves the user's workflow or outcome
- Why users will choose this solution

*Business Value*
One paragraph explaining:
- Revenue/retention/strategic impact
- Alignment with company goals
- Cost or risk of not building this

**3. User Stories**

Organize stories by priority tier:

*Must-Have (P0)*
Stories that block launch without them.

```
As a [user type], I want [action] so that [outcome].

Acceptance Criteria:
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3
```

*Should-Have (P1)*
Stories with significant value, targeted for initial release.

*Nice-to-Have (P2)*
Stories that enhance experience, can defer to fast-follow.

**4. UX & Design** (Optional)

Include one or more of:
- Links to Figma files/frames
- References to mockup files (with file paths)
- Key interaction descriptions
- Critical UX considerations
- Areas flagged for design attention

#### User Story Format Example

```
### Search Products by Keyword

As a **shopper**, I want to **search for products using keywords** 
so that **I can quickly find items I'm looking for**.

**Priority:** P0 (Must-Have)

**Acceptance Criteria:**
- [ ] Search input is prominently displayed on all pages
- [ ] Results appear within 2 seconds
- [ ] Results show product image, name, price
- [ ] Empty state shows helpful suggestions
- [ ] Search works with partial matches

**Notes:** Consider autocomplete for P1
```

#### Writing Style

**Clear and actionable:**
- Write for product and engineering teams
- Focus on user outcomes, not implementation
- Be specific about acceptance criteria
- Avoid ambiguous language

**What to include:**
- User context and motivation
- Measurable acceptance criteria
- Priority and rationale
- Dependencies and constraints
- Design references where available

**What to omit:**
- Technical implementation details
- Database schemas or API specs
- Sprint planning or estimates
- Detailed project timelines

## When to Stop the Workshop

You have sufficient information when you can clearly answer:

1. ✓ Who are we building for? (users are defined)
2. ✓ What problem are we solving? (value is clear)
3. ✓ Why does this matter to the business? (rationale is solid)
4. ✓ What are the requirements? (stories are complete with acceptance criteria)

Stop asking questions once these are answered. Write the PRD.

## Interaction Principles

**Be collaborative, not interrogative:**
- You're facilitating a workshop, not conducting an interview
- Invite discussion on priorities and scope
- Trust user's domain knowledge
- Challenge assumptions constructively

**Efficiency over completeness:**
- Don't over-engineer the conversation
- Focus on decisions that affect requirements
- Skip obvious or low-impact choices
- Keep scope manageable for V1

**Product-First documentation:**
- Remember your audience is product and engineering teams
- Focus on user outcomes and business value
- Provide enough context for autonomous implementation
- Keep technical decisions for the technical spec

## Example Workshop Flow

```
User: "I want to build a feature that lets users save products to wishlists"

Claude: "I'll help you create a PRD for that wishlist feature. Let me 
first check what's in your current project folder..."

[Runs discovery commands]

Claude: "I found your product one-pager and some Figma mockups in /designs. 
I see this is for your e-commerce platform. Before we define requirements, 
is there anything about your current user research or competitive analysis 
I should know?"

User: "We've seen 40% of users abandon carts—we think wishlists will help"

Claude: "That's useful context—wishlists as a cart abandonment solution. 
Who's the primary user for this feature?

A) Casual browsers (save for later, may not return)
B) Comparison shoppers (save multiple items, decide later)
C) Gift planners (save items for specific occasions)
D) Multiple personas—which should we prioritize?"

User: "B - comparison shoppers are our biggest segment"

Claude: "Got it. For comparison shoppers, which capability is most critical?

A) Basic save/remove (simple, fast to build)
B) Save with notes/tags (more organized, moderate effort)
C) Save with price tracking (high value, more complexity)
D) Something else—what matters most for comparison shopping?"

[Continues workshop through phases...]
```

## Adapting to Context

**For new products:**
- Spend more time on audience and value definition
- Be thorough with user story coverage
- Include competitive context in business rationale

**For feature additions:**
- Reference existing product context
- Focus on incremental user stories
- Connect to existing success metrics

**For improvements/iterations:**
- Start from current state pain points
- Keep story scope focused
- Emphasize measurable improvements
