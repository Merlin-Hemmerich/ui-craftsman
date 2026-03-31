# Design Rules

Strict rules to ensure high-quality output and prevent generic AI-generated designs.

---

## Core Principle

Every visible UI element must come from one of the three supported libraries (shadcn/ui, Cult UI, TripleD UI) and be used exactly as the library provides it. The goal is to leverage the design work already done by these libraries, not to reinvent it.

## Forbidden Actions

### Never modify component design code

The following must never be changed inside a component's source file:

- **Colors**: No changing `bg-*`, `text-*`, color tokens, gradients, or oklch values
- **Spacing**: No changing `p-*`, `m-*`, `gap-*`, `space-*` inside component internals
- **Border radius**: No changing `rounded-*` values inside components
- **Shadows**: No changing `shadow-*` values inside components
- **Animations**: No changing Framer Motion configs, `transition`, `animate`, `variants` objects
- **Typography**: No changing `text-*` size, `font-*` weight, `leading-*`, `tracking-*` inside components
- **Opacity**: No changing `opacity-*` values inside components

### Never build generic replacements

- No `div` with `rounded-xl border p-6 shadow-md` as a substitute for a Card component
- No custom Tailwind hero sections when Hero components exist in Cult UI or TripleD
- No hand-rolled pricing tables when Glassmorphism Pricing exists
- No custom testimonial layouts when Testimonials Block exists
- No manual animation code when Framer Motion components exist in the libraries

### Never mix component internals

- Do not inject a Cult UI button into a TripleD card's internal JSX structure
- Do not replace a shadcn/ui Dialog's internal content area with a Cult UI component
- Do not modify one library's component to accept another library's component as a child where not intended

### Never leave placeholder content

- No "Lorem ipsum" text
- No "Your Amazing Product" placeholder headings
- No "John Doe" placeholder names (unless the user provides no content)
- No stock descriptions like "We provide the best solutions for your business"
- If the user has not provided specific content, ask for it or use contextually appropriate text based on the project

## Allowed Actions

### Text content changes

- Headings, titles, subtitles
- Button labels and CTA text
- Descriptions, paragraphs, body text
- Navigation labels and menu items
- Form labels and placeholder text
- Alt text for images

### Props and data

- Setting documented component props (`variant`, `size`, `disabled`, `className` for layout only)
- Passing data arrays (items for carousels, testimonials arrays, pricing tier objects)
- Setting event handlers (`onClick`, `onSubmit`, etc.)
- Conditional rendering based on data

### Layout wrappers (outside components)

Tailwind classes are allowed ONLY on wrapper elements that arrange components on the page:

```tsx
// ALLOWED: Layout wrapper arranging components
<div className="grid grid-cols-1 md:grid-cols-2 gap-8 max-w-7xl mx-auto py-16 px-4">
  <TestimonialsBlock testimonials={data} />
  <StatsCounterBlock stats={stats} />
</div>

// FORBIDDEN: Custom-styled div replacing a component
<div className="rounded-2xl bg-gradient-to-r from-blue-500 to-purple-600 p-8 shadow-xl">
  <h2 className="text-4xl font-bold text-white">Our Features</h2>
  ...
</div>
```

### Combining libraries side by side

Components from different libraries may coexist on the same page as separate sections:

```tsx
// ALLOWED: Different libraries in separate page sections
<main>
  <HeroDithering />           {/* Cult UI */}
  <Separator />                {/* shadcn/ui */}
  <FeatureCardsGrid />         {/* TripleD */}
  <TestimonialsBlock />        {/* TripleD */}
  <NewsletterSignupBlock />    {/* TripleD */}
  <FooterBlock />              {/* TripleD */}
</main>
```

## Quality Checklist

Before presenting any UI output, verify:

1. Every visible component comes from one of the three libraries
2. No component source code was modified (check for design-related Tailwind class changes)
3. All text content is contextually appropriate (no placeholders)
4. Layout wrappers only contain positioning/spacing classes
5. No generic div-based UI was created where a library component exists
6. Components from different libraries are not mixed at the internal level

## Edge Cases

### When no component matches

If the user requests something not available in any of the three libraries:

1. State clearly that no matching component exists
2. List the closest available alternatives from the component map
3. Ask the user if one of the alternatives works
4. Do NOT build a custom replacement

### When the user explicitly asks for modifications

If the user specifically requests a design change to a component (e.g., "make the hero section blue"):

1. Explain that the skill's purpose is to use components as-is
2. Suggest checking if the component supports the change via props or theming
3. If the library's theming system supports it (e.g., shadcn CSS variables), apply it at the theme level — not in the component code
4. If it requires modifying component source, inform the user and ask for confirmation before proceeding

### When multiple components could work

When the component map shows multiple options for a use-case:

1. Consider the project's existing style (glassmorphism, minimal, neumorphism)
2. Prefer the component that best matches the overall page aesthetic
3. If unclear, present the top 2-3 options to the user with a brief description of each
