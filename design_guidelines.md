# Lua Obfuscator Design Guidelines

## Design Approach
**System-Based Approach** using principles from **VS Code + GitHub's code interface** combined with **Material Design** foundations. This utility-focused developer tool prioritizes clarity, code readability, and functional efficiency over visual flair.

## Core Design Principles
1. **Code-First Interface**: The code editor occupies primary screen real estate
2. **Developer Ergonomics**: Minimize friction, maximize productivity
3. **Clear Visual Hierarchy**: Input → Action → Output flow is immediately apparent
4. **Dark-Optimized**: Primary interface in dark theme with excellent contrast

---

## Typography System

**Monospace (Code):**
- Font: `'JetBrains Mono', 'Fira Code', 'Consolas', monospace` via Google Fonts
- Input/Output Code: text-sm (14px), leading-relaxed
- Line numbers: text-xs (12px), opacity-60

**Sans-Serif (UI):**
- Font: `'Inter', system-ui, sans-serif` via Google Fonts
- Headings: text-xl font-semibold (20px)
- Body/Labels: text-sm (14px)
- Buttons: text-sm font-medium

---

## Layout System

**Spacing Primitives**: Use Tailwind units of **2, 4, 6, 8** consistently
- Component padding: p-4, p-6
- Section gaps: gap-6, gap-8
- Button padding: px-6 py-2

**Grid Structure**: Single-column application layout with split-pane code areas

---

## Component Library

### Application Shell
**Header Bar** (sticky top):
- Full-width, h-14, border-b
- Left: Logo/Title "Lua Obfuscator" (text-xl font-semibold)
- Right: GitHub link icon, theme toggle (optional feature)
- Padding: px-6

### Main Workspace
**Two-Panel Code Editor**:
- Split layout: 50/50 on desktop, stacked on mobile
- Gap: gap-6 between panels
- Each panel structure:
  - Label bar: "Input Code" / "Obfuscated Output" (text-sm font-medium, pb-2)
  - Textarea/Display: min-h-96, rounded border, p-4
  - Monospace font throughout
  - Line numbers in left gutter (optional enhancement)

**Control Bar** (between panels on desktop, below input on mobile):
- Centered action area
- Primary button: "Obfuscate Code" (px-8 py-3, rounded, text-base font-medium)
- Secondary actions row (mt-4):
  - "Clear Input" (text button)
  - "Copy Output" (text button with icon)
  - Settings icon (opens options panel)
- Spacing: gap-4 between buttons

### Settings Panel (expandable below control bar)
**Obfuscation Options**:
- Checkbox list with labels:
  - "Rename variables" (checked by default)
  - "Rename functions" (checked by default)
  - "Encode strings" (checked by default)
  - "Remove comments" (checked by default)
  - "Minify whitespace" (checked by default)
- Compact layout: gap-3 between items
- Toggle to show/hide: "Advanced Options" button

### Output Display
**Code Block**:
- Read-only textarea styled as code display
- Background slightly different from input (subtle differentiation)
- Auto-height based on content (max-height with scroll)
- Top-right corner: "Copy" button overlay (absolute positioning)

### Footer
**Minimal Attribution**:
- Centered text: "Built with Replit" + link
- Small text: text-xs opacity-60
- Padding: py-8

---

## Interaction Patterns

**Code Input**:
- Textarea with syntax highlighting (use Prism.js or highlight.js)
- Tab key inserts spaces (not focus change)
- Line numbers optional but recommended

**Obfuscate Action**:
- Instant client-side processing
- Loading state on button during processing (if needed)
- Auto-scroll to output on completion

**Copy to Clipboard**:
- One-click copy with visual feedback
- Button text changes: "Copy" → "Copied!" (2 sec)

---

## Responsive Behavior

**Desktop (lg:)**
- Side-by-side panels: `grid grid-cols-2 gap-6`
- Control bar centered between panels
- Max width container: max-w-7xl mx-auto

**Tablet (md:)**
- Maintain side-by-side if space allows
- Reduce padding slightly

**Mobile (base):**
- Stack vertically: `grid grid-cols-1 gap-6`
- Control bar below input, above output
- Full-width panels
- Reduced padding: p-3 instead of p-4

---

## Visual Differentiation

**Panel Borders**: Subtle borders to define code areas
**Background Layers**: Three-tier depth (page bg → panel bg → active elements)
**Focus States**: Clear focus rings on textarea and buttons for accessibility
**Button States**: Defined hover/active states with subtle transforms

---

## Images
No images required for this application interface. This is a pure code editor tool where visual elements would distract from functionality.