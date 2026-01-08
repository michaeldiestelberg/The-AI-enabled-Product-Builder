---
name: narrative-presenter
description: Transform bullet point notes into an interactive narrative website for live presentations. Use this skill when the user wants to create a "presentation website" or "interactive narrative" from notes, or when they want to present ideas one argument at a time with animations. Creates a React artifact that reveals content progressively with click-to-advance navigation.
---

# Narrative Presenter

Transform bullet point notes into an interactive, animated website for live presentations. The output is a React artifact that reveals arguments one at a time, perfect for screen-sharing during talks, demos, or workshops.

## When to Use

This skill applies when the user:
- Provides bullet point notes and wants a presentation website
- Asks to "turn notes into a narrative"
- Wants to present ideas progressively (one point at a time)
- Needs an interactive website for a talk, demo, or workshop
- Mentions "narrative presenter" or "presentation website"

## Process

### Step 1: Analyze the Notes

Parse the user's bullet points to identify:

1. **Core arguments**: The main points or claims being made
2. **Supporting details**: Evidence, examples, or elaboration under each argument
3. **Narrative arc**: The logical flow from opening to conclusion
4. **Key transitions**: Where one idea leads to the next

### Step 2: Structure the Narrative

Transform bullets into presentation "beats" - discrete moments in the narrative:

**Beat types:**
- **Opening**: Sets context, poses a question, or creates tension
- **Argument**: A core claim or point
- **Evidence**: Supporting data, example, or illustration
- **Transition**: Bridges between major sections
- **Reveal**: A key insight or "aha" moment
- **Conclusion**: Synthesis, call to action, or closing thought

**Structuring rules:**
- Each beat should be digestible in 10-30 seconds of speaking
- Group related bullets into single beats when they form one complete thought
- Split dense bullets into multiple beats when they contain distinct ideas
- Add transitional beats to improve flow between major sections
- Create breathing room - not every beat needs heavy content

### Step 3: Create the React Artifact

**CRITICAL**: Before implementing, read the `frontend-design` skill (`/mnt/skills/user/frontend-design/SKILL.md`) and apply its principles. The presentation must be visually distinctive, not generic.

#### Required Features

1. **Accumulating Narrative**
   - Content builds up over time - previous beats remain visible
   - Each new beat appears as a card or box that joins the visible storyline
   - Future beats are completely hidden until revealed
   - NOT a slideshow - the audience sees the argument being constructed
   - Layout flows either top-to-bottom (vertical scroll) or left-to-right (horizontal scroll)

2. **Overflow Behavior**
   - When content exceeds the viewport, older beats scroll naturally out of view
   - The container auto-scrolls to keep the newest beat visible
   - Audience can still see the recent progression of the narrative
   - No manual scroll required - the view follows the presenter

3. **Navigation**
   - Click anywhere to advance (except on interactive elements)
   - Keyboard: Arrow keys or spacebar to navigate
   - Optional: Small progress indicator (dots or fraction)
   - Optional: Back navigation to revisit earlier beats

4. **Animations**
   - Each new beat animates in (fade, slide, scale, or creative combinations)
   - Use staggered reveals for multi-part beats
   - Smooth transitions (300-600ms typical)
   - Previous beats remain static once revealed

5. **Visual Hierarchy**
   - Main argument text should dominate within each card
   - Supporting details clearly subordinate
   - Visual distinction between beat types (different card styles)
   - Clear visual separation between beats (gaps, borders, or cards)

#### Technical Specifications

```jsx
// Core state structure
const [revealedCount, setRevealedCount] = useState(1); // Start with first beat visible
const containerRef = useRef(null);

const beats = [
  { type: 'opening', content: '...', subContent: '...' },
  { type: 'argument', content: '...', highlight: '...' },
  // ...
];

// Only show beats up to revealedCount
const visibleBeats = beats.slice(0, revealedCount);

// Navigation handlers
const advance = () => {
  if (revealedCount < beats.length) {
    setRevealedCount(prev => prev + 1);
  }
};
const goBack = () => setRevealedCount(prev => Math.max(prev - 1, 1));

// Auto-scroll to newest beat
useEffect(() => {
  if (containerRef.current) {
    containerRef.current.scrollTo({
      top: containerRef.current.scrollHeight, // or left for horizontal
      behavior: 'smooth'
    });
  }
}, [revealedCount]);

// Keyboard support
useEffect(() => {
  const handleKeyDown = (e) => {
    if (['ArrowRight', 'ArrowDown', ' '].includes(e.key)) {
      e.preventDefault();
      advance();
    }
    if (['ArrowLeft', 'ArrowUp'].includes(e.key)) goBack();
  };
  window.addEventListener('keydown', handleKeyDown);
  return () => window.removeEventListener('keydown', handleKeyDown);
}, [revealedCount]);
```

#### Layout Patterns

**Vertical flow (top-to-bottom):**
```jsx
<div 
  ref={containerRef}
  className="h-screen overflow-y-auto p-8 space-y-6"
  onClick={advance}
>
  {visibleBeats.map((beat, i) => (
    <BeatCard 
      key={i} 
      beat={beat} 
      isNew={i === visibleBeats.length - 1}
    />
  ))}
</div>
```

**Horizontal flow (left-to-right):**
```jsx
<div 
  ref={containerRef}
  className="h-screen overflow-x-auto flex gap-6 p-8 items-start"
  onClick={advance}
>
  {visibleBeats.map((beat, i) => (
    <BeatCard 
      key={i} 
      beat={beat} 
      isNew={i === visibleBeats.length - 1}
      className="flex-shrink-0 w-80"
    />
  ))}
</div>
```

**Card component with entrance animation:**
```jsx
const BeatCard = ({ beat, isNew, className }) => (
  <div 
    className={`
      rounded-xl p-6 bg-white/10 backdrop-blur
      ${isNew ? 'animate-slide-in' : ''}
      ${className}
    `}
  >
    <div className="text-sm uppercase tracking-wider opacity-60 mb-2">
      {beat.type}
    </div>
    <div className="text-2xl font-bold">
      {beat.content}
    </div>
    {beat.subContent && (
      <div className="mt-3 text-lg opacity-80">
        {beat.subContent}
      </div>
    )}
  </div>
);
```

#### Animation Approaches

**Entrance animation for new cards:**
```css
@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(30px); /* or translateX for horizontal */
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-slide-in {
  animation: slideIn 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
```

**Staggered reveals for multi-element beats:**
```jsx
// When a beat contains multiple items, stagger their appearance
{beat.items && beat.items.map((item, i) => (
  <div 
    key={i}
    style={{ 
      animationDelay: `${i * 150}ms`,
      animation: isNew ? 'slideIn 0.5s ease-out forwards' : 'none',
      opacity: isNew ? 0 : 1
    }}
  >
    {item}
  </div>
))}
```

**Subtle pulse on the newest card (optional):**
```css
@keyframes subtlePulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(255,255,255,0.1); }
  50% { box-shadow: 0 0 0 4px rgba(255,255,255,0.2); }
}

.newest-card {
  animation: subtlePulse 2s ease-in-out 0.5s;
}
```

#### Design Considerations

Apply `frontend-design` skill principles:

- **Typography**: Choose a bold, distinctive display font for arguments; readable body font for details
- **Color**: Commit to a cohesive palette that matches the content's tone (e.g., warm for personal stories, cool/technical for data-driven content)
- **Layout**: Use generous whitespace; center important text; consider asymmetric layouts for visual interest
- **Atmosphere**: Add subtle background elements (gradients, patterns, noise) to avoid flat design
- **Motion**: Make animations purposeful - they should enhance understanding, not distract

#### Beat Type Card Styles

Each beat type should have a distinct visual treatment as a card:

```jsx
// Opening card - dramatic, larger, sets the stage
<div className="opening-card bg-gradient-to-br from-indigo-900 to-purple-900 
                rounded-2xl p-8 border border-white/10">
  <div className="text-xs uppercase tracking-widest text-white/50 mb-4">Opening</div>
  <h1 className="text-4xl font-display font-bold text-white">
    {beat.content}
  </h1>
  {beat.subContent && (
    <p className="text-xl text-white/70 mt-4">{beat.subContent}</p>
  )}
</div>

// Argument card - bold, attention-grabbing
<div className="argument-card bg-white/10 backdrop-blur rounded-xl p-6 
                border-l-4 border-amber-400">
  <div className="text-xs uppercase tracking-widest text-amber-400/80 mb-2">Argument</div>
  <blockquote className="text-2xl font-bold text-white">
    {beat.content}
  </blockquote>
</div>

// Evidence card - contains multiple items in a grid
<div className="evidence-card bg-white/5 rounded-xl p-6">
  <div className="text-xs uppercase tracking-widest text-white/50 mb-4">Evidence</div>
  <div className="grid grid-cols-2 gap-4">
    {beat.items.map((item, i) => (
      <div key={i} className="bg-white/10 rounded-lg p-4 text-white/90">
        {item}
      </div>
    ))}
  </div>
</div>

// Reveal card - dramatic emphasis, centered
<div className="reveal-card bg-gradient-to-r from-rose-500 to-orange-500 
                rounded-2xl p-8 text-center">
  <div className="text-xs uppercase tracking-widest text-white/70 mb-4">Key Insight</div>
  <span className="text-5xl font-black text-white">
    {beat.highlight}
  </span>
</div>

// Conclusion card - final, prominent
<div className="conclusion-card bg-emerald-900/80 rounded-2xl p-8 
                border border-emerald-400/30">
  <div className="text-xs uppercase tracking-widest text-emerald-400/80 mb-4">Conclusion</div>
  <div className="text-3xl font-bold text-white">
    {beat.content}
  </div>
</div>
```

### Step 4: Output as Artifact

Create a single-file React artifact containing:
- All beat content as structured data
- Complete component with state management
- All styles (Tailwind utilities or inline CSS)
- Navigation logic and keyboard handlers
- Animations and transitions

**Important artifact settings:**
- Use React (.jsx extension)
- Include all dependencies inline
- Ensure it works standalone in the artifact viewer

## Example Transformation

**Input (user's notes):**
```
- AI is changing how we build products
- Traditional approach: humans write every requirement
- New approach: AI assists at every stage
- Three key workflows:
  - Voice memos → structured docs
  - Rough ideas → refined specs
  - Specs → working prototypes
- The compound effect: each step builds on the last
- Result: 10x faster from idea to MVP
```

**Output structure (beats):**
1. Opening: "AI is changing how we build products"
2. Argument: "Traditional approach: humans write every requirement" (with visual of old workflow)
3. Transition: "But what if AI could help at every stage?"
4. Argument: "The new approach: AI-assisted product building"
5. Evidence (3 cards): Voice memos → docs, Ideas → specs, Specs → prototypes
6. Reveal: "The compound effect"
7. Conclusion: "10x faster from idea to MVP"

## Quality Checklist

Before finalizing, verify:

- [ ] Content accumulates - previous beats remain visible
- [ ] Each beat appears as a distinct card/box
- [ ] New beats animate in smoothly
- [ ] Auto-scroll keeps newest beat visible
- [ ] Future content cannot be read ahead
- [ ] Navigation works (click + keyboard)
- [ ] Design is distinctive (not generic)
- [ ] Progress indicator is subtle but helpful
- [ ] Works well at typical presentation sizes (1080p+)
- [ ] Typography is bold and readable from distance
- [ ] Card styles clearly differentiate beat types
