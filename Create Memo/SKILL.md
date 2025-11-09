---
name: create-memo
description: This skill helps capture unstructured thoughts (via text or voice) across multiple turns and converts them into structured memos that are saved to a Notion inbox database. Use when the user wants to create a memo, capture thoughts, or provide content that should be documented verbatim without analysis or response.
---

# Create Memo

This skill enables capturing raw, unstructured thoughts (via text or voice input) across multiple conversational turns, then structuring those thoughts into a polished memo and saving it to a Notion inbox database.

## When to Use This Skill

Activate this skill when:
- User wants to create a memo or capture thoughts
- User says phrases like "Let's create a memo," "I want to capture some thoughts," "Let me dictate something," or similar
- User is clearly providing content that should be added to a running document rather than receiving conversational analysis or response
- User begins providing thoughts or ideas that should be documented verbatim

## Core Workflow

This skill has TWO distinct phases. Understanding when to switch between them is CRITICAL.

### Phase 1: Capture Mode (DEFAULT - STAY HERE)

**When to be in this phase:** By default, ALWAYS. This is where the skill spends 99% of its time.

**What to do:**
1. **Do NOT analyze, respond to, or act on the content** being provided
2. **Do NOT structure, process, or save to Notion yet**
3. Simply acknowledge with ONE of these short responses:
   - "Added."
   - "Got it."
   - "Captured."
   - "Added to the memo."
4. Internally accumulate all raw input verbatim
5. **Continue in Capture Mode for EVERY subsequent message** unless explicitly told to save

**Stay in Capture Mode Examples:**
- User: "Let's create a memo" → YOU: "Got it." → STAY IN CAPTURE MODE
- User: "I've been thinking about our product strategy" → YOU: "Added." → STAY IN CAPTURE MODE  
- User: "We need to improve the catalog structure" → YOU: "Captured." → STAY IN CAPTURE MODE
- User: "Also the search needs to be better" → YOU: "Added to the memo." → STAY IN CAPTURE MODE

**CRITICAL RULE**: Do NOT exit Capture Mode just because the user stops providing input or sends a complete thought. ALWAYS stay in Capture Mode until explicitly told to save/finalize.

### Phase 2: Finalization (ONLY WHEN EXPLICITLY REQUESTED)

**When to enter this phase:** ONLY when the user uses one of these EXPLICIT phrases:
- "Add this to Notion"
- "Save to my inbox"
- "Create the page"
- "Save this memo"
- "Done, save it"
- Similar explicit save/finalize commands

**Do NOT enter this phase when:**
- User simply stops talking/typing
- User sends a complete thought
- User pauses between messages
- You think they might be done

**Exit Capture Mode Examples (triggers for Phase 2):**
- User: "Add this to Notion" → NOW exit Capture Mode and finalize
- User: "Ok, save to my inbox" → NOW exit Capture Mode and finalize
- User: "Create the page now" → NOW exit Capture Mode and finalize

**What to do in Phase 2:**

#### Step 1: Structure the Content

Review all captured raw input and create a structured version:

**Remove:**
- Self-corrections (e.g., "no wait, I meant...")
- Verbal fillers and thinking pauses (e.g., "um," "uh," "let me think") - these may appear in voice transcriptions
- Dictation/typing artifacts and false starts
- Repetitive statements that were corrected later

**Preserve:**
- ALL substantive information and ideas
- The user's voice and intent
- Key details, even if mentioned tangentially
- The natural flow of thought (just cleaned up)

**Structure:**
Choose the most appropriate format based on the content:
- Narrative paragraphs for conceptual thinking
- Bullet points for lists or action items
- Sections with headings for multi-topic memos
- Mixed format as needed for clarity

Keep the tone professional but natural.

#### Step 2: Create Final Document

Create a document with two distinct sections:

```
[Structured Memo Content]

---
## Raw Notes (Original Input)
---

[All original unstructured input verbatim]
```

The structured memo goes on top, followed by a clear separator, then the raw notes at the bottom for reference.

#### Step 3: Save to Notion

1. **Generate Title**: Create a concise, descriptive title in Title Case that captures the memo's essence (typically 5-10 words)

2. **Create Notion Page**: 
   - Use database ID: `1f566a9ce05280dbaf7ae5f5e93a571f`
   - Set the title property with the generated title
   - Add the complete document (structured memo + raw notes) as the page content
   - Use the Notion MCP tools to create the page

3. **Confirm Success**: After successful creation, output:
   ```
   I've created your memo and added it to your Notion inbox:
   
   [View in Notion](notion-page-link)
   
   The title is: "[Generated Title in Title Case]"
   ```

## Complete Interaction Example

**User:** "Let's create a memo"  
**Assistant:** "Got it."  
*(Capture Mode active)*

**User:** "I've been thinking about how we could improve our product catalog structure. Right now we have too many nested categories."  
**Assistant:** "Added."  
*(Still in Capture Mode)*

**User:** "Maybe we should flatten the hierarchy but keep two levels max."  
**Assistant:** "Captured."  
*(Still in Capture Mode)*

**User:** "Also the search needs to use AI not just keywords."  
**Assistant:** "Added to the memo."  
*(Still in Capture Mode)*

**User:** "Save to my inbox"  
**Assistant:** *[NOW exits Capture Mode, structures content, creates document, saves to Notion]*  
"I've created your memo and added it to your Notion inbox:

[View in Notion](link)

The title is: 'Product Catalog Structure And Search Improvements'"

## Important Reminders

- **Default to Capture Mode**: When in doubt, stay in Capture Mode with a simple acknowledgment
- **Explicit triggers only**: Only finalize when user explicitly asks to save/add to Notion
- **No assumptions**: Never assume the user is done just because they sent a complete thought
- **Preserve everything**: The raw notes section must contain all original input for reference
- **Quality titles**: Generate titles that are specific and informative, not generic
- **No metadata**: Do not add any additional Notion page properties beyond the title