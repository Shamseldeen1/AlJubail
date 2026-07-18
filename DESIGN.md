# Design

Visual system for the record page (سجل توظيف). Direction: **Official minimal** — a flawlessly typeset official-form idiom. Near-white page, dark green-tinted ink, one deep institutional green accent.

## Color

OKLCH, restrained strategy: tinted neutrals plus a single accent used sparingly.

| Token | Value | Role |
|---|---|---|
| `--bg` | `oklch(0.985 0.002 155)` | Page background — true off-white, faint green tint |
| `--ink` | `oklch(0.24 0.02 155)` | Body text, values, headings |
| `--ink-muted` | `oklch(0.45 0.02 155)` | Field labels, meta text (passes 4.5:1 on `--bg`) |
| `--accent` | `oklch(0.42 0.08 155)` | Title rule, section marks, focus ring, print button |
| `--accent-deep` | `oklch(0.34 0.07 155)` | Button hover |
| `--hairline` | `--ink` at 14% alpha | Rules and dividers |
| `--hairline-soft` | `--ink` at 8% alpha | Dotted leaders |

The accent never appears as large fills except the print button. No gradients, no shadows heavier than a whisper.

## Typography

- **IBM Plex Sans Arabic** 400 / 500 / 700 — all Arabic text, headings, labels, UI.
- **IBM Plex Mono** 500 — digit-only values (residency, commercial registration, subscription numbers) and dates in mono contexts.
- Fixed rem scale, ratio ≈ 1.2: 13px labels/meta → 15.5px letter body → 16px values → 19px section heads (h2) → 27px title (h1).
- Letter prose: line-height ≈ 2, max-measure 68ch, `text-wrap: pretty`.
- Never letter-space or uppercase Arabic script. Mono digits may carry slight tracking.

## Layout

- Single centered column, sheet max-width 680px, page padding 56px top / 64px bottom.
- Title row: h1 + bordered "نسخة شخصية" pill, short accent rule beneath, meta line with the letter date.
- Sections separated by hairline rules and generous space (48px rhythm), each headed by an h2 with a small accent square.
- Fields are **dotted-leader rows** (`<dl>`): label at the inline start, dotted leader filling the middle, value at the inline end. Below 480px the leader hides and the value stacks under its label.
- Letter text: indented quiet block with a hairline inline-start border (1px — not a side-stripe accent).
- Footer: letter date (mono) and the طباعة / حفظ PDF button.

## Components

- **Badge**: 1px `--hairline` border pill, `--ink-muted` text, no fill.
- **Print button**: `--accent` fill, white text, 44px min target, hover → `--accent-deep`, `:focus-visible` 2px accent outline offset 2px, active nudge 1px. Transitions 160ms ease-out; disabled under reduced motion.
- **Field row**: dt (muted, 13px 500) · leader (dotted hairline) · dd (ink, 16px 700; `.num` = Plex Mono 15px 500).

## Motion

Hover/focus transitions only, 160ms `cubic-bezier(0.25, 1, 0.5, 1)`. No entrance choreography, no scroll effects. `prefers-reduced-motion: reduce` removes all transitions and transforms.

## Print

`@media print`: flat white, no shadow or border-radius on the sheet, button hidden, `@page` margin 14mm, exact-color adjust on accent elements. Output must read as a clean A4 personal record.
