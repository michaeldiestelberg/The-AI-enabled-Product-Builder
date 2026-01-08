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
- **Context**: Background information or setup
- **Insight**: A mental model or framework with icon
- **Tip**: Practical advice with emoji icon
- **Transition**: Bridges between major sections
- **Phase**: Numbered section headers for multi-part frameworks
- **Reveal**: A key insight or "aha" moment
- **Conclusion/Closing**: Synthesis, call to action, or closing thought

**Structuring rules:**
- Each beat should be digestible in 10-30 seconds of speaking
- Group related bullets into single beats when they form one complete thought
- Split dense bullets into multiple beats when they contain distinct ideas
- Add transitional beats to improve flow between major sections
- Create breathing room - not every beat needs heavy content

### Step 3: Create the React Artifact

#### Required Features

1. **Accumulating Narrative**
   - Content builds up over time - previous beats remain visible
   - Each new beat appears as a card or box that joins the visible storyline
   - Future beats are completely hidden until revealed
   - NOT a slideshow - the audience sees the argument being constructed
   - Layout flows top-to-bottom (vertical scroll)

2. **Scroll Behavior**
   - When content exceeds the viewport, use `scrollIntoView` with `block: 'center'`
   - This keeps the newly revealed beat centered in the viewport
   - Audience can see recent context above and has room below
   - Smooth scrolling behavior for professional feel

3. **Navigation**
   - Click anywhere to advance (except on interactive elements like links/buttons)
   - Keyboard: Arrow keys, spacebar, or Enter to navigate
   - Back button to revisit earlier beats
   - Progress indicator showing current position (e.g., "5 / 20" with visual bar)

4. **Animations**
   - Each new beat animates in with fade + slide up (translateY)
   - Use 0.5s ease-out timing for smooth entrance
   - Previous beats remain static once revealed

5. **Visual Hierarchy**
   - Main argument text should dominate within each card
   - Supporting details clearly subordinate
   - Visual distinction between beat types (different card styles)
   - Clear visual separation between beats

---

## Default Design System: Editorial Warmth

Unless the user specifies a different style, use this refined editorial design. It features warm earth tones, classic typography, and a sophisticated paper-like aesthetic.

### Color Palette

```javascript
// Primary colors
const colors = {
  // Backgrounds
  pageBg: 'from-stone-100 via-amber-50/30 to-stone-100', // gradient
  cardBg: 'bg-white',
  contextBg: 'bg-amber-50',
  phaseBg: 'bg-stone-800',
  revealBg: 'from-amber-600 to-orange-700', // gradient
  
  // Text
  headingText: 'text-stone-800',
  bodyText: 'text-stone-500',
  subtleText: 'text-stone-400',
  accentText: 'text-amber-700',
  labelText: 'text-amber-600',
  
  // Borders & accents
  cardBorder: 'border-stone-200',
  contextBorder: 'border-amber-200',
  accentBorder: 'border-amber-500',
  progressActive: 'bg-amber-500',
  progressInactive: 'bg-stone-300',
};
```

### Typography

```css
/* Use Georgia serif for all headings and key content */
font-family: 'Georgia, serif'

/* Font weights */
- Headings: font-light to font-medium (not bold, elegant feel)
- Body: default weight
- Labels: font-medium with uppercase tracking-widest
- Phase numbers: font-black (for watermark effect)
```

### Layout Structure

```jsx
// Page wrapper
<div className="min-h-screen bg-gradient-to-b from-stone-100 via-amber-50/30 to-stone-100 cursor-pointer select-none">
  
  {/* Subtle dot pattern overlay */}
  <div 
    className="fixed inset-0 pointer-events-none opacity-40"
    style={{
      backgroundImage: `radial-gradient(circle at 1px 1px, rgba(120, 113, 108, 0.15) 1px, transparent 0)`,
      backgroundSize: '24px 24px'
    }}
  />
  
  {/* Fixed header with progress */}
  <div className="fixed top-0 left-0 right-0 z-20 bg-gradient-to-b from-stone-100 via-stone-100/95 to-transparent pb-8 pt-4">
    {/* Progress bar content */}
  </div>
  
  {/* Main content area */}
  <div className="relative z-10 max-w-3xl mx-auto px-6 pt-20 pb-32">
    <div className="space-y-6">
      {/* Beats render here */}
    </div>
  </div>
  
  {/* Fixed footer with navigation hints */}
  <div className="fixed bottom-0 left-0 right-0 z-20 bg-gradient-to-t from-stone-100 via-stone-100/95 to-transparent pt-8 pb-4">
    {/* Back button and keyboard hint */}
  </div>
</div>
```

### Beat Type Styles

#### Opening
```jsx
<div className="text-center py-16">
  <h1 className="text-5xl md:text-7xl font-light tracking-tight text-stone-800 mb-3" 
      style={{ fontFamily: 'Georgia, serif' }}>
    {beat.content}
  </h1>
  <p className="text-xl md:text-2xl text-amber-700 font-light max-w-xl mx-auto leading-relaxed" 
     style={{ fontFamily: 'Georgia, serif' }}>
    {beat.subContent}
  </p>
</div>
```

#### Argument
```jsx
<div className="bg-white rounded-2xl shadow-sm border border-stone-200 p-8 md:p-10">
  <h2 className="text-2xl md:text-3xl font-medium text-stone-800 mb-3 leading-snug" 
      style={{ fontFamily: 'Georgia, serif' }}>
    {beat.content}
  </h2>
  <p className="text-lg text-stone-500 leading-relaxed">
    {beat.subContent}
  </p>
</div>
```

#### Reveal (Key Insight)
```jsx
<div className="bg-gradient-to-br from-amber-600 to-orange-700 rounded-2xl p-8 md:p-12 text-white shadow-lg">
  {beat.label && (
    <p className="text-sm text-amber-200 uppercase tracking-widest mb-2">
      {beat.label}
    </p>
  )}
  <h2 className="text-4xl md:text-6xl font-bold mb-4" style={{ fontFamily: 'Georgia, serif' }}>
    {beat.content}
  </h2>
  {beat.subContent && (
    <p className="text-lg text-amber-100 leading-relaxed max-w-xl">
      {beat.subContent}
    </p>
  )}
</div>
```

#### Phase (Numbered Section)
```jsx
<div className="bg-stone-800 rounded-2xl p-8 md:p-10 text-white relative overflow-hidden">
  {/* Large watermark number */}
  <div className="absolute top-4 right-6 text-8xl font-black text-white/5" 
       style={{ fontFamily: 'monospace' }}>
    {beat.phase}
  </div>
  <div className="relative z-10">
    <p className="text-sm text-amber-400 uppercase tracking-widest mb-2">
      Phase {beat.phase}
    </p>
    <h2 className="text-3xl md:text-4xl font-medium text-white mb-3" 
        style={{ fontFamily: 'Georgia, serif' }}>
      {beat.content}
    </h2>
    <p className="text-lg text-stone-300 leading-relaxed">
      {beat.subContent}
    </p>
  </div>
</div>
```

#### Context
```jsx
<div className="bg-amber-50 rounded-2xl p-8 md:p-10 border border-amber-200">
  <p className="text-xl md:text-2xl text-stone-700 font-light leading-relaxed" 
     style={{ fontFamily: 'Georgia, serif' }}>
    {beat.content}
  </p>
</div>
```

#### Insight (with icon)
```jsx
<div className="bg-white rounded-2xl shadow-sm border border-stone-200 p-8 md:p-10">
  <div className="flex items-start gap-6">
    <div className="text-5xl flex-shrink-0">{beat.icon}</div>
    <div>
      <h2 className="text-2xl md:text-3xl font-medium text-stone-800 mb-3" 
          style={{ fontFamily: 'Georgia, serif' }}>
        {beat.content}
      </h2>
      <p className="text-lg text-stone-600 leading-relaxed">
        {beat.subContent}
      </p>
      {beat.footnote && (
        <p className="text-base text-amber-700 mt-4 border-l-2 border-amber-500 pl-4 italic">
          {beat.footnote}
        </p>
      )}
    </div>
  </div>
</div>
```

#### Tip (Pro Tip)
```jsx
<div className="bg-gradient-to-r from-stone-100 to-amber-50 rounded-2xl p-8 border border-stone-200">
  <div className="flex items-start gap-4">
    <span className="text-3xl">{beat.icon}</span>
    <div>
      <p className="text-sm text-amber-600 uppercase tracking-widest mb-2 font-medium">Pro Tip</p>
      <p className="text-lg text-stone-700 leading-relaxed" style={{ fontFamily: 'Georgia, serif' }}>
        {beat.content}
      </p>
    </div>
  </div>
</div>
```

#### Evidence (List with cards)
```jsx
<div className="bg-white rounded-2xl shadow-sm border border-stone-200 p-8 md:p-10">
  <p className="text-sm text-stone-400 uppercase tracking-widest mb-6">
    {beat.content}
  </p>
  <div className="space-y-4">
    {beat.items.map((item, i) => (
      <div 
        key={i}
        className={`p-5 rounded-xl border ${
          item.recommended 
            ? 'bg-amber-50 border-amber-300' 
            : 'bg-stone-50 border-stone-200'
        }`}
      >
        <div className="flex items-start justify-between gap-4">
          <div>
            <span className={`text-lg font-medium ${
              item.recommended ? 'text-amber-800' : 'text-stone-700'
            }`} style={{ fontFamily: 'Georgia, serif' }}>
              {item.name}
            </span>
            <p className="text-stone-500 mt-1">{item.desc}</p>
          </div>
          {item.recommended && (
            <span className="flex-shrink-0 px-2 py-1 bg-amber-500 text-white text-xs font-bold uppercase tracking-wider rounded">
              ✓
            </span>
          )}
        </div>
      </div>
    ))}
  </div>
  {beat.footnote && (
    <p className="text-base text-amber-700 mt-6 border-l-2 border-amber-500 pl-4 italic">
      {beat.footnote}
    </p>
  )}
</div>
```

#### Transition
```jsx
<div className="text-center py-10">
  <h2 className="text-3xl md:text-4xl font-light text-stone-600 mb-2" 
      style={{ fontFamily: 'Georgia, serif' }}>
    {beat.content}
  </h2>
  {beat.subContent && (
    <p className="text-lg text-amber-600 font-mono">{beat.subContent}</p>
  )}
</div>
```

#### Closing
```jsx
<div className="text-center py-12">
  <h2 className="text-4xl md:text-5xl font-medium text-stone-800 mb-4" 
      style={{ fontFamily: 'Georgia, serif' }}>
    {beat.content}
  </h2>
  <p className="text-xl text-amber-600 font-light max-w-lg mx-auto leading-relaxed" 
     style={{ fontFamily: 'Georgia, serif' }}>
    {beat.subContent}
  </p>
</div>
```

### Progress Bar Component

```jsx
{/* In fixed header */}
<div className="max-w-3xl mx-auto px-6 flex justify-between items-center">
  <div className="text-sm text-stone-500 font-mono">
    {visibleBeats} / {beats.length}
  </div>
  <div className="flex items-center gap-1">
    {beats.map((_, i) => (
      <div 
        key={i}
        className={`h-1.5 rounded-full transition-all duration-300 ${
          i < visibleBeats 
            ? 'w-6 bg-amber-500' 
            : 'w-1.5 bg-stone-300'
        }`}
      />
    ))}
  </div>
</div>
```

### Animation

```jsx
<style>{`
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  .animate-fade-in {
    animation: fadeIn 0.5s ease-out forwards;
  }
`}</style>
```

---

## Custom Styles

If the user requests a different style (e.g., "dark mode", "tech/cyberpunk", "minimalist", "playful"), read the `frontend-design` skill (`/mnt/skills/user/frontend-design/SKILL.md`) and apply its principles to create a distinctive design that matches the requested aesthetic while maintaining the same structural patterns and beat types.

When customizing:
- Keep the same beat type structure and navigation patterns
- Adapt colors, typography, and visual effects to match the requested style
- Maintain readability and presentation-friendly sizing
- Ensure sufficient contrast for screen-sharing scenarios

---

## Technical Specifications

### Core State Structure

```jsx
const [visibleBeats, setVisibleBeats] = useState(1);
const [animatingBeat, setAnimatingBeat] = useState(0);
const containerRef = useRef(null);
const lastBeatRef = useRef(null);

const beats = [
  { type: 'opening', content: '...', subContent: '...' },
  { type: 'argument', content: '...', subContent: '...' },
  { type: 'phase', phase: '01', content: '...', subContent: '...' },
  { type: 'evidence', content: '...', items: [...], footnote: '...' },
  { type: 'reveal', label: '...', content: '...', subContent: '...' },
  // ...
];
```

### Navigation Handlers

```jsx
const advance = () => {
  if (visibleBeats < beats.length) {
    setAnimatingBeat(visibleBeats);
    setVisibleBeats(prev => prev + 1);
  }
};

const goBack = () => {
  if (visibleBeats > 1) {
    setVisibleBeats(prev => prev - 1);
  }
};

// Scroll to center the latest beat
useEffect(() => {
  if (lastBeatRef.current) {
    lastBeatRef.current.scrollIntoView({ 
      behavior: 'smooth', 
      block: 'center'
    });
  }
}, [visibleBeats]);

// Keyboard support
useEffect(() => {
  const handleKeyDown = (e) => {
    if (['ArrowRight', ' ', 'Enter', 'ArrowDown'].includes(e.key)) {
      e.preventDefault();
      advance();
    }
    if (['ArrowLeft', 'ArrowUp'].includes(e.key)) {
      e.preventDefault();
      goBack();
    }
  };
  window.addEventListener('keydown', handleKeyDown);
  return () => window.removeEventListener('keydown', handleKeyDown);
}, [visibleBeats]);

// Click handler (exclude links and buttons)
const handleClick = (e) => {
  if (e.target.tagName !== 'A' && e.target.tagName !== 'BUTTON') {
    advance();
  }
};
```

### Step 4: Output as Artifact

Create a single-file React artifact containing:
- All beat content as structured data array
- Complete component with state management
- All styles (Tailwind utilities + inline CSS for animations)
- Navigation logic and keyboard handlers
- Default editorial design unless user specifies otherwise

**Important artifact settings:**
- Use React (.jsx extension)
- Include all dependencies inline
- Ensure it works standalone in the artifact viewer

---

## Quality Checklist

Before finalizing, verify:

- [ ] Content accumulates - previous beats remain visible
- [ ] Each beat appears as a distinct card/box with appropriate styling
- [ ] New beats animate in smoothly (fade + slide up)
- [ ] Auto-scroll centers the newest beat in viewport
- [ ] Future content cannot be read ahead
- [ ] Navigation works (click + keyboard + back button)
- [ ] Progress indicator shows current position
- [ ] Uses default editorial design (stone/amber palette, Georgia serif) unless custom style requested
- [ ] Works well at typical presentation sizes (1080p+)
- [ ] Typography is readable from distance
- [ ] Beat type styles clearly differentiate content types
