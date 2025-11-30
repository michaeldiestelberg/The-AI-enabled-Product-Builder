# Create Memo Skill

A Claude skill (compatible with ChatGPT and Gemini) that records typed or dictated thoughts as raw memo content and converts them into polished, structured documents ready for your notes app. Designed for product builders who need a reliable “thought-to-note” pipeline without manual transcription.

![Create Memo Example](create-memo_example.png)

## Configuration

- Claude
    - Review the SKILL.md file and modify it as needed
    - Add the Notion database ID to the SKILL.md file if you want to make use of storing the memo in Notion (this will make the MCP tool use faster)
    - Add SKILL.md to a zip archive and upload the skill to Claude (for web and app use)
- ChatGPT
    - Copy the contents of chatgpt.md and add it as an instruction to your custom GPT
    - Alternatively, use my shared GPT: [Create Memo GPT](https://chatgpt.com/g/g-6921d74c5bb48191a1c485e5d9d29e93-create-memo)
- Gemini
    - Copy the contents of gemini.md and add it as an instruction to your custom Gem
    - Alternatively, use my shared Gem: [Create Memo Gem](https://gemini.google.com/gem/1fSXFQ9_TQwOY0cXEFJM4yupmf0hWrNB1?usp=sharing)

For full context and usage walkthrough, see my "The AI-enabled Product Builder" resource: [Never Lose an Idea Again: My AI Voice-to-Notes System](https://productized.tech/the-ai-enabled-product-builder/voice-to-notes)