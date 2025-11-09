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

## How to Use This Skill

**CRITICAL**: Once this skill is activated, immediately enter Capture Mode. Do NOT have a conversation about creating a memo or ask what the user wants to capture. The activation itself (user saying "let's create a memo" or similar) IS the signal to start capturing. Begin with Capture Mode acknowledgments immediately.

### Phase 1: Capture Mode (Default State)

When the user is providing thoughts or content to capture:

1. **Do NOT analyze, respond to, or act on the content** being provided
2. Simply acknowledge receipt and internally maintain the raw input verbatim
3. Use minimal, neutral acknowledgments:
   - "Added."
   - "Got it."
   - "Captured."
   - "Added to the memo."
4. Continue in capture mode across multiple conversational turns
5. Accumulate all input exactly as provided (whether typed or spoken), preserving everything

**Important**: Treat ALL input as content to capture, regardless of whether it's typed text or voice transcription. The user's intent is to build a document, not to have a conversation about the content.

### Phase 2: Finalization (User-Triggered)

When the user explicitly requests to save the memo to Notion (phrases like "add this to Notion," "save to my inbox," "create the page," etc.):

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
   - Use database ID: `YOUR_DATABASE_ID_HERE`
   - Set the title property with the generated title
   - Add the complete document (structured memo + raw notes) as the page content
   - Use the Notion MCP tools to create the page

3. **Confirm Success**: After successful creation, output:
   ```
   I've created your memo and added it to your Notion inbox:
   
   [View in Notion](notion-page-link)
   
   The title is: "[Generated Title in Title Case]"
   ```

## Important Notes

- **Stay in character**: Remain in capture mode by default. Do not break character to discuss, question, or analyze the content being dictated
- **Transition only when requested**: Only move to finalization when the user explicitly asks to save to Notion
- **Preserve everything**: The raw notes section must contain all original input for reference
- **Quality titles**: Generate titles that are specific and informative, not generic (e.g., "Product Catalog Structure Improvements" not "Meeting Notes")
- **No metadata**: Do not add any additional Notion page properties beyond the title
- **Format flexibility**: Let the content guide the structure—don't force a format that doesn't fit the material
