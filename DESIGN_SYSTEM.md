# Profile Design System

This document records the current design decisions for the profile page. It is a working source of truth: update it when a tested page decision becomes reusable.

## 1. Design principles

### Editorial before decorative

The page should read like a clear point of view, not a dashboard. Large statements establish hierarchy; supporting copy stays concise.

### Structure creates character

Use the grid, spacing, typography and contrast to create identity. Do not add decorative shapes, gradients or colors to compensate for weak hierarchy.

### Images must carry meaning

Use existing product or project imagery when it reveals the work. Otherwise use a quiet dark surface. Do not introduce generic illustrations or atmospheric stock imagery.

### Repetition builds rhythm

Cards in the same series share dimensions, internal structure and alignment. Content may vary without changing the layout.

## 2. Grid

- Page maximum width: `1440px`
- Desktop page padding: `48px`
- Tablet page padding: `32px`
- Mobile page padding: `20px`
- Desktop grid: `12` equal columns
- Grid gutter: `24px`
- Section split: introduction `4` columns, content `8` columns
- Tablet split: introduction `5` columns, content `7` columns
- Mobile: single column

Section introductions align to the first grid column. Card series begin on column 5 on desktop.

The header, hero and main content use the same `1440px` frame and the same responsive horizontal padding. Full-width backgrounds may extend beyond it, but readable content should remain aligned to this frame.

## 3. Spacing

Use a base unit of `4px`.

| Token | Value | Typical use |
| --- | ---: | --- |
| `space-1` | `4px` | Tight text relationships |
| `space-2` | `8px` | Small internal gaps |
| `space-3` | `12px` | Card series gap |
| `space-4` | `16px` | Standard control spacing |
| `space-6` | `24px` | Card padding and grid gutter |
| `space-8` | `32px` | Content groups |
| `space-10` | `40px` | Mobile section split |
| `space-20` | `80px` | Mobile page rhythm |
| `space-28` | `112px` | Tablet page rhythm |
| `space-36` | `144px` | Desktop section rhythm |

Prefer these values. Introduce an intermediate value only when the optical result requires it.

## 4. Typography

### Families

- Primary: `Inter`
- Editorial accent: `Instrument Serif`

Inter carries navigation, metadata, body copy, section statements, card titles and project overlays.

Outside the hero, Instrument Serif has exactly two uses:

1. First-person editorial copy, currently the Experience introduction.
2. Large Experience numbering.

Do not use it as a generic accent elsewhere.

### Scale

All type sizes use semantic CSS tokens. Do not introduce a raw size in a component.

| Token | Value | Primary role |
| --- | --- | --- |
| `type-meta` | `11px` | Labels, periods, card metadata |
| `type-caption` | `12px` | Captions and footer copy |
| `type-small` | `13px` | Secondary copy, links and controls |
| `type-body` | `15px` | Body copy and Experience roles |
| `type-editorial` | `23px` | First-person Instrument Serif copy |
| `type-index` | `36px` | Instrument Serif Experience index |
| `type-company` | `38px` | Experience company name |
| `type-tagline` | `28–38px` | Hero tagline |
| `type-project` | `34–52px` | Project card title |
| `type-overlay` | `40–56px` | Project overlay title |
| `type-section` | `38–60px` | Section statement |

Responsive section statements use `42px` on mobile and `36px` on compact mobile screens.

Rules:

- Use letter spacing `0` for new typography.
- Keep display type for true section statements and project names.
- Keep metadata short, uppercase only when it improves scanning.
- Keep body text on the `13px` or `15px` steps; do not introduce intermediate `14px` or `16px` values.
- Do not scale type directly with viewport width; use `clamp()` with fixed minimum and maximum values.

## 5. Color tokens

The palette is intentionally neutral.

| Token | Value | Role |
| --- | --- | --- |
| `bg` | `#212121` | Page background |
| `surface` | `#131416` | Dark media and overlays |
| `accent` | `#ffffff` | Strong text and active elements |
| `text` | `#e2e2e2` | Primary text on dark |
| `text-dim` | `#999999` | Secondary text on dark |
| `text-muted` | `#666666` | Quiet metadata |
| Card surface | `#f5f5f5` | Light cards |
| Card hover | `#ffffff` | Hover/focus feedback |
| Card ink | `#111111` | Text on light cards |
| Border | `rgba(255,255,255,0.22)` | Lines on dark |

Do not add a new hue unless it represents project content inside an image.

## 6. Background

- Use a fixed ghost grid aligned to the readable content frame.
- Desktop and tablet use `12` vertical columns.
- The decorative grid and content grid share the same `24px` gutter token.
- Decorative column starts repeat at `column width + gutter`, not at `container width / 12`.
- Column starts use a vertical dotted rhythm rather than continuous rules.
- Real gutters receive a subtle `135deg` hatch pattern.
- Construction guides remain monochrome.
- Mobile uses `4` vertical columns.
- Horizontal guides use a wider rhythm: `96px` desktop and `80px` mobile.
- Dots remain below `6%` white opacity.
- Gutter hatching remains below `3%` white opacity.
- Horizontal and frame guides remain below `4%` white opacity.
- Add a monochrome noise texture at very low opacity to soften the technical quality of the grid.
- Opaque cards naturally hide the grid; do not add extra masks around content.

## 7. Shape and depth

- Large surface radius: `48px` for hero panels, cards, overlay panels and large previews
- Media radius: `32px` for images, videos and media areas
- Control radius: `24px` for compact links and app icons
- Pill radius: `999px`
- Large surfaces use `40px` internal padding so content stays clear of curved corners
- Compact mobile surfaces may reduce this inset to `32px`
- Icon button shape: circle
- Cards use contrast and a small `translateY(-4px)` interaction instead of decorative shadows.
- Avoid cards inside cards. A media area is part of its parent card, not a nested card.

## 8. Section pattern

Each major content section uses:

1. A compact category label.
2. A strong editorial statement.
3. One short supporting paragraph.
4. A repeated content series aligned to the right side of the grid.

On mobile, the introduction moves above the series.

## 9. Experience cards

- Cards form a vertical stack in the content side of the section grid
- Each card is a single edge-to-edge surface split into two zones
- Desktop uses a horizontal composition: period panel on the left, content panel on the right
- The left panel uses the period tag's light gray surface
- The right panel is white and contains company, role and index
- There is no gap or outer padding between the zones
- The white panel overlaps the gray panel by `24px` and carries the rounded intersection
- The Instrument Serif index appears in white inside a dark circular marker
- Mobile stacks the zones vertically and keeps the same `24px` overlap
- Do not invent company imagery or logos without a meaningful source

## 10. Project cards

- Two columns on wide screens
- One column on tablet
- Horizontal snap series on mobile
- Order: project metadata, title and description, media
- The media area uses a square `1:1` aspect ratio
- Media uses real project assets only and fills its container with `object-fit: cover`
- The media block repeats the card radius on its upper corners
- Entire card opens the project detail overlay

## 11. Responsive behavior

### Desktop: above `1024px`

- 12-column grid
- Experience appears as a vertical card list
- Projects use two columns

### Tablet: `761–1024px`

- 12-column grid with a `5/7` section split
- Projects stack in one column

### Mobile: `760px` and below

- Single-column section layout
- Experience remains a vertical list
- Projects become a horizontal snap series
- A partial next card should remain visible to communicate scrollability
- Page content must not create horizontal document overflow

## 12. Interaction and accessibility

- Interactive cards are keyboard focusable.
- `Enter` and `Space` open project overlays.
- `Escape`, backdrop click and the close button dismiss overlays.
- Hover and focus-visible states should communicate the same hierarchy.
- Images that are purely decorative use an empty `alt`.
- Respect stable card dimensions so loading media does not shift the layout.
