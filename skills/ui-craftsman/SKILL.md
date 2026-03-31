---
name: UI Craftsman
description: This skill should be used when the user asks to "build a landing page", "create a dashboard", "add a hero section", "make a pricing table", "build a contact form", "create a testimonials section", "add a navbar", "build a sidebar", "create a card layout", "add animations", "build a footer", or any request involving frontend UI component creation, page building, or section design.
---

# UI Craftsman

Build polished, production-grade frontend UI by using components from three libraries exactly as designed. Never generate generic AI-slop layouts. Every UI element must come from one of the three supported libraries and be used 1:1 without modifying its design code.

## Supported Libraries

| Library | Strength | Registry Prefix |
|---------|----------|-----------------|
| **shadcn/ui** | Base components: Buttons, Forms, Tables, Cards, Dialogs, Navigation | (none) |
| **Cult UI** | Animated components: Hero sections, text effects, interactive cards, marketing | `@cult-ui/` |
| **TripleD UI** | Motion blocks: Landing pages, dashboards, glassmorphism, full sections | `@uitripled/` |

## Workflow

For every UI request, follow these 4 steps in order:

### Step 1: Analyze the Request

Determine what is needed. Break down the request into individual UI components and sections. Identify the type: landing page, dashboard, form, single component, full page, etc.

### Step 2: Consult the Component Map

Read `references/component-map.md`. Find the best matching component for each part of the request. Always prefer a pre-built component over building from scratch.

### Step 3: Install Components

Run the exact CLI commands from the component map. Verify the project has shadcn/ui initialized first. If not, consult `references/installation-guide.md` for setup.

### Step 4: Implement

Use each component exactly as provided by the library. Only change:
- Text content (headings, labels, descriptions, button text)
- Data (arrays, objects passed as props)
- Props (variant, size, and other documented props)

Never change:
- Colors, gradients, or color tokens inside component code
- Spacing, padding, or margin values inside component code
- Border radius or shadow values inside component code
- Animation parameters or Framer Motion configs inside component code
- Font sizes or typography inside component code

## Critical Rules

### What to do when no component matches

If no component from any of the three libraries matches the request, inform the user clearly:

> "No matching component found in shadcn/ui, Cult UI, or TripleD UI for [request]. Available alternatives: [list closest matches]."

Do NOT improvise a custom Tailwind layout. Do NOT build a generic div-soup replacement.

### Combining components from different libraries

Components from different libraries may be placed **side by side** as separate sections on a page. For example, a shadcn/ui Sidebar next to a Cult UI Hero Section is fine — they occupy different areas.

Never mix component internals across libraries. Do not put a Cult UI button inside a TripleD card's internal structure.

### Layout wrappers

Tailwind utility classes are allowed ONLY for arranging components on the page:
- `grid`, `flex`, `gap-*` for layout
- `container`, `max-w-*`, `mx-auto` for page width
- `py-*`, `px-*` on wrapper `div`s between sections
- `min-h-screen`, `relative`, `overflow-hidden` for page structure

These wrappers hold components in place. They do not replace components.

## Additional Resources

### Reference Files

For detailed component listings and rules, consult:
- **`references/component-map.md`** — Complete mapping: Use-Case to Component to Library to CLI command
- **`references/design-rules.md`** — Detailed rules for quality output, anti-patterns, and edge cases
- **`references/installation-guide.md`** — Setup instructions for all three libraries and registry configuration
