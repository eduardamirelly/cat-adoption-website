# KITT8-BIT Component Guidelines

This document outlines the rules and conventions for creating new components in the **KITT8-BIT Cat Adoption Platform**. Adhere strictly to these patterns to maintain the unified "Nostalgic Gallery" aesthetic that bridges low-fi 8-bit charm and high-end editorial clarity.

## 1. Golden Rules of Construction

### The "No-Line" Rule
- **Never use 1px standard web borders** (`border-1`, `border-t`, etc.).
- Separation **must be achieved through background shifts** (e.g., placing a `bg-surface` element on a `bg-surface-container-low` background).
- If a border is absolutely necessary, it must be **4px or 8px thick** to mimic the blocky pixel-art scaling (e.g. `border-4` or `border-b-4`).
- **Never use `rounded-md`, `rounded-lg`, etc.** All `border-radius` values must be `0px`.

### 8-Bit Pixel Steps
- If grouping lists (such as process steps or cards on a grid), generate division lines by using thick gaps (e.g., `gap-1` natively maps to 4px spacing in standard Tailwind configuration). 
- When placing standard components inside a grey parent container (`bg-surface-container-low`), a `gap-1` creates a perfect 4px "Pixel Step" separator between elements.

## 2. Structural Composition

### Astro Components Structure
- Keep logic and presentation separated where possible.
- Use `Props` interface declarations rigorously in the frontmatter:
  ```ts
  export interface Props {
    title: string;
    variant?: "primary" | "secondary";
  }
  ```

### Functional Styling
Use Tailwind classes in the following order of mental hierarchy:
1. Position / Display / Flex grid classes (e.g. `relative flex flex-col md:flex-row`)
2. Spacing / Padding / Gap (e.g. `p-8 gap-6`)
3. Backgrounds and Surfaces (`bg-surface`)
4. Typography (`font-display font-bold text-2xl uppercase text-on-surface`)
5. Effects / Interactions (`hover:pixel-shadow transition-none`)

**Class Normalization (`suggestCanonicalClasses`):**
- Always use canonical Tailwind classes to prevent linter warnings.
- For example, use `grow` instead of `flex-grow`, `shrink` instead of `flex-shrink`, etc.

## 3. Topography & Elevation

Depth in KITT8-BIT is a product of nested color density, never blurry drop shadows.

### Tonal Stacking
Leverage the predefined design tokens:
- **`bg-surface`**: The primary backdrop (warm cream).
- **`bg-surface-container-low`**: Used for backing grouped content blocks.
- **`bg-surface-container-lowest`**: Applied to cards or elevated interactive elements to contrast hard against the rest.

### Pixel Shadows
DO NOT use Tailwind's default `shadow` or `shadow-md` classes (which are blurry). KITT8-BIT has custom utility classes defined for sharp 8-bit shadows:
- Example: the project uses solid-color pixel offset patterns for lift.
- Always apply standard pixel offsets instead of blurred variants.

## 4. Typography Protocols

- **Display & Headings:** Use `font-display` (Space Grotesk) strictly combined with `uppercase` and tight tracking (`tracking-tight`).
- **Body Context:** Use `font-body` (Plus Jakarta Sans). Keep it fully legible and structured with `leading-relaxed` for heavy text areas.
- **Pixel Accents:** The 8-bit aesthetic primarily manifests in accents and labels. Use `font-pixel` (Press Start 2P) paired with `uppercase` and generous spacing (`tracking-widest`). Do not set paragraphs in pixel fonts.

## 5. Adding New Elements Example

If building a new UI piece, like a `Tag` component:
- **Don't**: `<div class="rounded-full border border-gray-300 text-sm shadow">`
- **Do**: `<div class="bg-tertiary-fixed font-pixel text-[10px] uppercase p-2 border-b-4 border-surface-container-highest">`

---

## 6. Modular & Reusable Components

Every component must be **self-contained, purposeful, and reusable**. Think of each `.astro` file as a Lego brick — it should do one thing well and snap into any layout without friction.

### 6.1 Single Responsibility

Each component should solve **one problem**. If a component is doing too many things, split it.

```
✅ Good: <StepCard /> renders a single process step.
❌ Bad:  <JourneySection /> renders the title, steps, background, and footer all in one 400-line file.
```

### 6.2 File Size & Readability

- Aim for **under 80 lines** per component file.
- If a component grows beyond that, extract sub-components.
- Prefer readable class groupings over one-liners with 20+ classes crammed together.

```astro
<!-- ✅ Readable: Attributes on separate lines when there are many classes -->
<div
  class="flex flex-col gap-4 p-8 bg-surface-container-lowest border-b-4 border-surface-container-highest"
>
  <slot />
</div>

<!-- ❌ Avoid: hard to scan at a glance -->
<div class="flex flex-col gap-4 p-8 bg-surface-container-lowest border-b-4 border-surface-container-highest"><slot /></div>
```

### 6.3 Naming Conventions

| Pattern | Example | Use when |
|---|---|---|
| `PascalCase` file names | `StepCard.astro` | All Astro components |
| Descriptive + specific | `CatProfileCard.astro` | Avoid generic names like `Card.astro` |
| Variant via prop, not file | `<Button variant="ghost" />` | Instead of `GhostButton.astro` |

---

## 7. Props & Composition Patterns

### 7.1 Explicit Props via TypeScript Interface

Always declare a typed `Props` interface. This serves as the component's public API contract — it makes the component self-documenting.

```ts
// ✅ Clear, typed, and optional flags are explicit
export interface Props {
  title: string;
  description?: string;
  step: number;
  highlighted?: boolean;
}

const { title, description, step, highlighted = false } = Astro.props;
```

### 7.2 Lean on `<slot />` for Flexibility

Prefer `<slot />` over forcing consumers to pass content as props. This keeps components presentation-agnostic and easier to compose.

```astro
<!-- ✅ Flexible: consumer controls the inner content -->
<SectionWrapper>
  <StepCard title="Find" step={1} />
  <StepCard title="Meet" step={2} />
</SectionWrapper>

<!-- ❌ Rigid: component assumes too much about its children -->
<JourneySection steps={[{ title: "Find", step: 1 }, { title: "Meet", step: 2 }]} />
```

### 7.3 Named Slots for Structured Layouts

For complex layout components that have distinct regions (e.g., header, body, footer), use **named slots**:

```astro
<!-- Layout component -->
<div class="flex flex-col bg-surface">
  <header class="p-8 bg-surface-container-low">
    <slot name="header" />
  </header>
  <main class="p-8">
    <slot />
  </main>
</div>

<!-- Consumer -->
<PageLayout>
  <h1 slot="header">Adopt a Cat</h1>
  <CatGrid />
</PageLayout>
```

---

## 8. Component Checklist

Before marking a component as complete, verify:

- [ ] **Single responsibility** — it does one thing and does it clearly.
- [ ] **Under 80 lines** — or has been split into logical sub-components.
- [ ] **Typed `Props` interface** — all props declared and destructured with defaults.
- [ ] **No 1px borders** — separation achieved through background color shifts or 4px/8px borders.
- [ ] **No `rounded-*` classes** — `border-radius` is always `0`.
- [ ] **No blurry shadows** — only pixel-shadow utilities or no shadow at all.
- [ ] **Canonical Tailwind classes** — e.g., `grow` not `flex-grow`.
- [ ] **Correct font usage** — `font-display`, `font-body`, or `font-pixel` as appropriate.
- [ ] **Uses `<slot />`** — for flexible, composable content injection where applicable.
