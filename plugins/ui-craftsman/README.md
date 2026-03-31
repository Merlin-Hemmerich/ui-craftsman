# UI Craftsman

**A Claude Code plugin that builds polished, production-grade frontend UI — no generic AI slop.**

Instead of generating cookie-cutter Tailwind layouts, UI Craftsman uses real components from three best-in-class shadcn-registry libraries and applies them 1:1 without modifying their design code.

---

## The Problem

AI coding assistants produce generic, repetitive UI:
- Same `rounded-xl border p-6 shadow` card everywhere
- Hand-rolled hero sections that all look the same
- Custom Tailwind layouts instead of using existing, polished components
- Placeholder-heavy output that needs complete redesign

## The Solution

UI Craftsman forces Claude to use **real components from real design libraries** — exactly as their designers intended. Only text content and data get changed. The design stays untouched.

---

## Supported Libraries

| Library | Components | Focus |
|---------|-----------|-------|
| [**shadcn/ui**](https://ui.shadcn.com) | 100+ | Foundation: Buttons, Forms, Tables, Cards, Dialogs |
| [**Cult UI**](https://www.cult-ui.com) | 70+ | Animations, effects, marketing sections |
| [**TripleD UI**](https://ui.tripled.work) | 137 | Motion blocks, landing pages, glassmorphism |

All three are **shadcn-registry-based** — fully compatible, same installation pattern.

---

## Installation

### Option 1: CLI Flag

```bash
claude --plugin-dir /path/to/ui-craftsman
```

### Option 2: Permanent (Settings)

Add to your Claude Code settings (`~/.claude/settings.json`):

```json
{
  "plugins": [
    "/path/to/ui-craftsman"
  ]
}
```

### Option 3: Project-Level

Add to your project's `.claude/settings.json`:

```json
{
  "plugins": [
    "/path/to/ui-craftsman"
  ]
}
```

---

## How It Works

When you ask Claude to build UI, the skill activates and follows 4 steps:

### 1. Analyze Request
Breaks down what you need — hero section, dashboard, pricing page, etc.

### 2. Consult Component Map
Looks up the best matching component from ~200 mapped components across all three libraries, organized by use-case.

### 3. Install
Runs the exact CLI command to add the component:

```bash
# shadcn/ui base components
npx shadcn@latest add button card dialog

# Cult UI animated components
npx shadcn@beta add @cult-ui/hero-dithering @cult-ui/texture-card

# TripleD motion blocks
npx shadcn-ui@latest add @uitripled/glassmorphism-hero @uitripled/testimonials-block
```

### 4. Implement
Uses the component **exactly as designed**. Only changes:
- Text content (headings, labels, descriptions)
- Data (arrays, objects passed as props)
- Documented props (variant, size, etc.)

**Never changes:** colors, spacing, animations, typography, or any design code inside components.

---

## Component Categories

The skill maps ~200 components across 18 categories:

| Category | Examples |
|----------|---------|
| Hero Sections | Dithering, Color Panels, Waves, Glassmorphism, Liquid Metal |
| Navigation | Sidebar, Nav Menu, Command Palette, macOS Dock, Floating Panel |
| Cards | Expandable, Shift, Texture, Minimal, Neumorphism, Browser Window |
| Buttons | Cosmic, Morphing, Liquid, Texture, Gradient, Neumorphism |
| Forms | Input, Select, Date Picker, Color Picker, OTP, Popover Form |
| Tables & Data | Data Table, Sortable List, Stats Counter, Stocks Dashboard |
| Dialogs | Dialog, Alert Dialog, Sheet, Drawer, Bottom Modal, Family Drawer |
| Typography | Gradient Heading, Pixel Text, Typewriter, Flip Text, Text GIF |
| Media | 3D Carousel, Hover Video, YouTube Player, Gallery Lightbox |
| Marketing | Testimonials, Pricing, CTA, FAQ, Newsletter, Logo Carousel |
| Dashboard | Full Dashboard, Bento Grid, Services Grid, Minimal Metrics |
| Animations | Magnetic, Follow Cursor, Terminal Animation, Avatar Expand |
| Backgrounds | Texture Overlay, Fractal Grid, Shader Blur, LightBoard |
| Onboarding | Onboarding Flow, Feature Carousel, Intro Disclosure |
| Page Sections | About Us, Team, Timeline, Footer, Blog, Portfolio |
| Interactive | Poll, Vote Tally, Prompt Library, AI Instructions, Code Block |
| Layout | Resizable Panels, Scroll Area, Accordion, Collapsible |
| Feedback | Toast, Alert, Badge, Tooltip, Skeleton, Notification Bell |

---

## Design Rules

### What the skill does NOT do

- Modify component source code (colors, spacing, animations, typography)
- Build generic Tailwind layouts when a library component exists
- Create `div`-soup replacements for real components
- Mix component internals across libraries
- Leave "Lorem ipsum" placeholder text
- Improvise when no matching component exists

### What the skill DOES do

- Select the best component for each use-case from the component map
- Install via the correct CLI command
- Use components exactly as designed
- Arrange components on pages using Tailwind layout wrappers (grid, flex, gap)
- Place components from different libraries side-by-side as separate sections
- Ask the user when no matching component exists

---

## Example Usage

```
You: "Build me a landing page for a SaaS product"

Claude (with UI Craftsman):
1. Installs Hero Dithering (Cult UI) for the hero
2. Installs Feature Cards Grid (TripleD) for features
3. Installs Glassmorphism Pricing (TripleD) for pricing
4. Installs Testimonials Block (TripleD) for social proof
5. Installs Newsletter Signup Block (TripleD) for lead capture
6. Installs Footer Block (TripleD) for the footer
→ All components used 1:1, only text content customized
```

```
You: "Create a dashboard with stats and a data table"

Claude (with UI Craftsman):
1. Installs Sidebar (shadcn/ui) for navigation
2. Installs Stats Counter Block (TripleD) for metrics
3. Installs Data Table (shadcn/ui) for the table
4. Installs Badge (shadcn/ui) for status indicators
5. Installs Dropdown Menu (shadcn/ui) for row actions
→ Clean dashboard, no generic card grids
```

---

## Project Setup

Before using UI Craftsman, your project needs shadcn/ui initialized:

```bash
# 1. Initialize shadcn/ui
npx shadcn@latest init -d

# 2. Add Cult UI registry to components.json
# (the skill handles this automatically)

# 3. Install Framer Motion (required by Cult UI + TripleD)
npm install framer-motion
```

---

## Plugin Structure

```
ui-craftsman/
├── .claude-plugin/
│   └── plugin.json                  # Plugin manifest
├── skills/
│   └── ui-craftsman/
│       ├── SKILL.md                 # Core skill instructions
│       └── references/
│           ├── component-map.md     # ~200 components mapped by use-case
│           ├── design-rules.md      # Quality rules and anti-patterns
│           └── installation-guide.md # Setup for all 3 libraries
└── README.md
```

---

## Contributing

Want to add more components to the map? Edit `skills/ui-craftsman/references/component-map.md` and add new entries following the existing format:

```markdown
| Use-Case | Component | Library | CLI Command |
|----------|-----------|---------|-------------|
| Your use case | Component Name | Library Name | `npx shadcn@... add ...` |
```

---

## License

MIT

---

Built by [Hemmerich Consulting](https://github.com/hemmerich-consulting)
