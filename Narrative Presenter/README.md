# Narrative Presenter

A Claude skill that transforms bullet point notes into interactive presentation websites.

## What it does

Paste your notes → Get a React artifact that builds up your narrative visually, one argument at a time. Each point appears as a card that stays visible, creating a storyline your audience can follow as you speak.

**Features:**
- Accumulating layout - previous points stay visible as cards
- Click anywhere or use arrow keys to reveal the next point
- Smooth animations as new cards appear
- Auto-scrolls to keep the latest point visible
- Distinctive, non-generic design

## Installation

1. Download `SKILL.md`
2. In Claude.ai, go to **Settings → Profile → Claude skills**
3. Upload the file

## Usage

Paste your bullet points and ask Claude to create a "narrative presenter" or "presentation website."

## Example

**Input:**
```
- AI is changing product development
- Old way: humans write everything
- New way: AI assists at every stage
- Result: 10x faster from idea to MVP
```

**Output:** An interactive React artifact with animated beats you click through while presenting.

## Dependencies

Works best with the [frontend-design](https://github.com/anthropics/courses/tree/master/prompt_engineering_interactive_tutorial/skills/frontend-design) skill for enhanced visual quality.

## License

MIT
