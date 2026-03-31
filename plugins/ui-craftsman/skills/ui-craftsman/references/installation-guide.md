# Installation Guide

Setup instructions for all three UI libraries in a Next.js project.

---

## Prerequisites

- Node.js 18+ installed
- A Next.js project (App Router recommended)
- Tailwind CSS configured

## Step 1: Initialize shadcn/ui

shadcn/ui is the foundation. Initialize it first:

```bash
npx shadcn@latest init -d
```

This creates `components.json` and sets up the `cn()` utility.

## Step 2: Configure Cult UI Registry

Add the Cult UI registry to `components.json`:

```json
{
  "registries": {
    "@cult-ui": {
      "url": "https://cult-ui.com/r/{name}.json"
    }
  }
}
```

Install Cult UI components:

```bash
npx shadcn@beta add @cult-ui/[component-name]
```

### Common Cult UI dependencies

Most Cult UI components require Framer Motion:

```bash
npm install framer-motion
```

## Step 3: Configure TripleD UI Registry

TripleD UI components are installed via the shadcn CLI with the `@uitripled` prefix:

```bash
npx shadcn-ui@latest add @uitripled/[component-name]
```

### Common TripleD dependencies

TripleD components often require:

```bash
npm install framer-motion
```

## Step 4: Verify Setup

After setup, the project should have:

```
project/
├── components.json          # shadcn config with registries
├── components/
│   └── ui/                  # shadcn base components
├── tailwind.config.ts       # Tailwind configuration
├── app/
│   └── globals.css          # CSS variables and theme
└── lib/
    └── utils.ts             # cn() utility
```

## Installing Components

### shadcn/ui (base components)

```bash
npx shadcn@latest add button card dialog input
```

### Cult UI (animated components)

```bash
npx shadcn@beta add @cult-ui/hero-dithering @cult-ui/texture-card
```

### TripleD UI (motion blocks)

```bash
npx shadcn-ui@latest add @uitripled/glassmorphism-hero @uitripled/testimonials-block
```

## Theming

All three libraries respect shadcn/ui's CSS variable theming. To change the global look:

### Dark mode (recommended for dashboards)

```tsx
// app/layout.tsx
<html lang="en" className="dark">
```

### Custom accent color

Edit `globals.css` and change `--color-primary`:

```css
@theme inline {
  --color-primary: oklch(0.488 0.243 264.376);
}
```

This affects all shadcn/ui components automatically. Cult UI and TripleD components that reference shadcn tokens also pick up the change.

## Troubleshooting

### Component not found

If a CLI command fails with "component not found":

1. Check the component name spelling in the component map
2. Verify the registry URL in `components.json` is correct
3. Try clearing the shadcn cache: `rm -rf node_modules/.cache/shadcn`

### Framer Motion errors

If components show animation errors:

```bash
npm install framer-motion@latest
```

### CSS conflicts between libraries

All three libraries use Tailwind CSS. If styles conflict:

1. Check that `tailwind.config.ts` includes all component paths in `content`
2. Ensure `globals.css` has the correct CSS variables
3. Do not override component-level styles — the libraries handle their own styling

### Registry authentication errors

If a registry requires authentication:

```json
{
  "registries": {
    "@cult-ui": {
      "url": "https://cult-ui.com/r/{name}.json",
      "headers": {
        "Authorization": "Bearer ${REGISTRY_TOKEN}"
      }
    }
  }
}
```
