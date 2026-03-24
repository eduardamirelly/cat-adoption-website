# Design System Specification



## 1. Overview & Creative North Star

### Creative North Star: "The Nostalgic Gallery"

This design system bridges the gap between low-fi 8-bit charm and high-end editorial clarity. We are not building a "video game" website; we are building a premium adoption platform that uses pixel art as a sophisticated design language rather than a novelty.



The system breaks the "template" look by utilizing heavy intentional asymmetry and a "Lo-Fi High-Res" contrast. By pairing rigid, pixelated display elements with expansive whitespace and organic cat photography, we create a visual rhythm that feels both playful and professional. Every element should feel "carved" out of a grid, yet floating in a calm, modern void.



---



## 2. Colors & Surface Architecture

The palette is a sophisticated departure from traditional primary-color 8-bit styles. We utilize warm creams and muted slate tones to let the photography provide the emotional "pop."



### Surface Hierarchy & Nesting

Instead of traditional lines, we use a "Tonal Stacking" method to define regions.

- **Base Layer:** `surface` (#faf9f6) is the canvas for the entire experience.

- **Content Blocks:** Use `surface_container_low` (#f4f3f1) for large sections to subtly ground the content.

- **Interactive Layers:** Use `surface_container_lowest` (#ffffff) for cards or inputs to make them "lift" off the page naturally.



### The "No-Line" Rule

**Strict Mandate:** Designers are prohibited from using 1px solid CSS borders to section off content.

- Separation must be achieved through background shifts (e.g., a `surface_container_high` sidebar against a `surface` main body).

- For the 8-bit aesthetic, "borders" are interpreted as **Pixel-Steps**: a 4px or 8px offset in background color that creates a blocky, stepped silhouette without a thin stroke.



### Signature Textures

Main CTAs and hero backgrounds should utilize a subtle vertical gradient from `primary` (#455565) to `primary_container` (#5d6d7e). This adds a "matte finish" feel that elevates the flat pixel aesthetic into the premium space.



---



## 3. Typography

The typographic strategy relies on a high-contrast pairing: a rigid, monospaced pixel font for "moments" and a fluid, accessible sans-serif for "information."



* **Display & Headlines (Space Grotesk):** While the user requested pixel fonts, we use **Space Grotesk** for large displays to maintain a "Tech-Modern" edge. To achieve the 8-bit feel, we apply a `text-transform: uppercase` and tight letter-spacing.

* **Body & Labels (Plus Jakarta Sans):** All long-form content uses **Plus Jakarta Sans**. Its geometric clarity ensures that even when surrounded by pixelated elements, the critical information (cat age, temperament, medical history) is perfectly legible.

* **The Pixel Accent:** Use a pixel-style font (like *Press Start 2P*) exclusively for small "UI Labels" (e.g., "STATUS: ADOPTED" or "NEW ARRIVAL"). This acts as a brand stamp rather than a primary reading font.



---



## 4. Elevation & Depth

In this system, depth is a product of color density, not shadows.



* **The Layering Principle:** Stack `surface_container` tiers. Place a `surface_container_lowest` card atop a `surface_container_low` section. This creates a soft, natural lift that mimics fine paper.

* **Ambient Shadows:** For floating modals, use a "Pixel Shadow." Instead of a blur, use a solid 4px offset to the bottom-right using `on_surface` at 8% opacity. This honors the 8-bit grid while remaining "Modern Minimalist."

* **Glassmorphism & Depth:** Navigation bars and floating filters must use `surface` with a `0.8` opacity and a `backdrop-blur: 12px`. This allows the vibrant cat photography to bleed through the UI, softening the rigid pixelated edges.



---



## 5. Components



### Buttons

- **Primary:** Solid `primary` background with `0px` border-radius. Instead of a shadow, use a 4px bottom-edge inset of `primary_fixed_variant` to create a "pressed" 8-bit look.

- **Secondary:** `surface_container_highest` background. Use "Ghost Borders"—a 2px border using `outline_variant` at 20% opacity.

- **States:** On hover, the button should shift 2px up and 2px left, with a solid pixel-shadow appearing behind it.



### Cards (The "Cat Profile")

- **Structure:** No borders. A `surface_container_lowest` container.

- **The "Step" Header:** The image at the top of the card should be clipped with an 8-bit "staircase" corner (e.g., a custom mask-image) to reinforce the theme without cluttering the UI.

- **Spacing:** Use Spacing Scale `6` (2rem) for internal padding to ensure the "Minimalist" feel is maintained.



### Input Fields

- **Styling:** Use `surface_container_low` with a bottom-only "Pixel Stroke" (4px height) in `primary`.

- **Error State:** Shift the bottom stroke to `error`. Do not use red text for the label; keep the label `on_surface_variant` to maintain the calm palette.



### Chips & Tags

- Small, rectangular blocks using `tertiary_fixed` with `label-sm` text. These should look like tiny 8-bit "inventory items."



---



## 6. Do's and Don'ts



### Do

- **DO** use generous whitespace (Spacing Scale `16` and `20`) between sections. The 8-bit look can feel "busy"; whitespace is your decompression chamber.

- **DO** use "Pixel-Art" icons for functional metaphors (a heart for likes, a paw for adoption) but keep them monochromatic using `primary`.

- **DO** align all elements to a strict 4px or 8px grid to ensure the "pixel" logic feels intentional and not accidental.



### Don'ts

- **DON'T** use rounded corners (`0px` radius only). Even a 2px radius breaks the retro-modern illusion.

- **DON'T** use 1px divider lines. If you need to separate content, use a background color jump from `surface` to `surface_container_lowest`.

- **DON'T** use bright neons. If the UI feels too "loud," revert to the `background` (#faf9f6) and `on_surface_variant` (#43474c) for a more editorial, muted tone.

- **DON'T** use drop shadows with large blurs. If depth is needed, use a solid-color offset or tonal layering.