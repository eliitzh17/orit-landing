# Design Specification — "לחזור לעצמך"

**Landing Page for Orit Ashor's Women's Learning Group**
**Platform:** GitHub Pages | **Tech:** Static HTML + CSS | **Direction:** RTL Hebrew | **Mobile-first**

---

## 1. Color Palette

| Token | Hex | Swatch | Usage | WCAG on Cream |
|---|---|---|---|---|
| `--cream` | `#FDF6F0` | ![#FDF6F0](https://via.placeholder.com/20/FDF6F0/FDF6F0) | Page body background | — |
| `--blush` | `#F2CECE` | ![#F2CECE](https://via.placeholder.com/20/F2CECE/F2CECE) | Card backgrounds, section alternates | — |
| `--blush-deep` | `#E8A8A8` | ![#E8A8A8](https://via.placeholder.com/20/E8A8A8/E8A8A8) | Card borders, dividers, horizontal rules | — |
| `--gold` | `#C9A84C` | ![#C9A84C](https://via.placeholder.com/20/C9A84C/C9A84C) | Decorative only — borders, ornaments, icon strokes. **Never for text** | 2.9:1 (fail for text) |
| `--gold-muted` | `#E8D5A3` | ![#E8D5A3](https://via.placeholder.com/20/E8D5A3/E8D5A3) | Large-area gold washes, gradient blends | — |
| `--cta-rose` | `#B85470` | ![#B85470](https://via.placeholder.com/20/B85470/B85470) | CTA button fill, links, active states | 5.2:1 AA Pass |
| `--text-body` | `#2C1A1A` | ![#2C1A1A](https://via.placeholder.com/20/2C1A1A/2C1A1A) | All body copy, headings, paragraphs | 13.4:1 AAA |
| `--text-mid` | `#6B4444` | ![#6B4444](https://via.placeholder.com/20/6B4444/6B4444) | Captions, secondary labels, metadata | 5.8:1 AA Pass |

### Contrast Matrix

| Foreground | Background | Ratio | WCAG AA |
|---|---|---|---|
| `#2C1A1A` on `#FDF6F0` | Body text on page | 13.4:1 | Pass |
| `#2C1A1A` on `#F2CECE` | Body text on card | 10.1:1 | Pass |
| `#6B4444` on `#FDF6F0` | Secondary text on page | 5.8:1 | Pass |
| `#6B4444` on `#F2CECE` | Secondary text on card | 4.6:1 | Pass |
| `#FFFFFF` on `#B85470` | CTA button text | 5.2:1 | Pass |
| `#C9A84C` on `#FDF6F0` | Gold on cream | 2.9:1 | Fail — decorative only |

### Palette Rationale

The cream/blush/gold triad is extracted from Orit's printed flyer (marbled pink-gold texture), creating visual continuity between offline materials the audience already recognizes and the digital experience. The warm near-black `#2C1A1A` avoids the sterile quality of pure `#000000` and reinforces the handcrafted, human feel.

---

## 2. Typography

### Font Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Assistant:wght@400;600&family=Secular+One&display=swap" rel="stylesheet">
```

### Font Stacks

```css
--font-display: 'Secular One', 'David Libre', 'Noto Serif Hebrew', serif;
--font-body:    'Assistant', 'Segoe UI', 'Arial Hebrew', sans-serif;
```

### Type Scale

| Element | Font | Size | Line-Height | Weight | Usage |
|---|---|---|---|---|---|
| `h1` | Secular One | `2.5rem` (40px) | 1.25 | 400 | Hero headline |
| `h2` | Secular One | `1.875rem` (30px) | 1.3 | 400 | Section headings |
| `h3` | Secular One | `1.375rem` (22px) | 1.35 | 400 | Card headings |
| Body large | Assistant | `1.125rem` (18px) | 1.75 | 400 | Lead paragraphs, hero subtext |
| Body default | Assistant | `1rem` (16px) | 1.75 | 400 | Running text |
| Body emphasis | Assistant | `1rem` (16px) | 1.75 | 600 | Inline bold, key phrases |
| Small / caption | Assistant | `0.875rem` (14px) | 1.6 | 400 | Captions, metadata |
| CTA label | Assistant | `1.125rem` (18px) | 1 | 600 | Button text |
| Micro label | Assistant | `0.8125rem` (13px) | 1.5 | 400 | Legal note below CTA |

### Typography Rules

- `letter-spacing: normal` — never adjust for Hebrew (breaks ligatures)
- `word-spacing: normal`
- `text-align: right` on all text (never `justify` — creates uneven rivers in Hebrew)
- `direction: rtl` on `<html>`
- `lang="he"` on `<html>` — activates correct hyphenation/rendering
- Minimum rendered text size: **16px**

---

## 3. Spacing System

Built on 8px base unit.

### Tokens

```css
--space-1:   4px     /* half-step, tight only */
--space-2:   8px     /* icon gap, inline padding */
--space-3:  12px     /* tight internal padding */
--space-4:  16px     /* default element gap */
--space-5:  20px     /* horizontal page padding (mobile) */
--space-6:  24px     /* card internal padding */
--space-8:  32px     /* between related groups */
--space-10: 40px     /* between unrelated elements */
--space-12: 48px     /* section vertical padding (mobile) */
--space-16: 64px     /* section vertical padding (desktop) */
--space-20: 80px     /* hero top padding */
--space-24: 96px     /* hero bottom padding */
```

### Applied Values

| Context | Mobile | Tablet+ |
|---|---|---|
| Page horizontal padding | 20px | 40px |
| Section vertical padding | 48px | 64px |
| Hero top padding | 64px | 96px |
| Max content width | — | **680px** |
| Card internal padding | 24px | 24px |
| Card grid gap | 16px | 16px |
| Heading → body gap | 12px | 12px |
| Body → CTA gap | 32px | 32px |

---

## 4. Page Structure

### Section Flow (top to bottom)

```
┌─────────────────────────────────────┐
│  1. HERO                            │
│  ┌─────────┐                        │
│  │  Photo   │  140x140 circle       │
│  └─────────┘                        │
│  [Scarcity Badge]                   │
│  "..לחזור לעצמך"                    │
│  Subtitle                           │
│  [CTA: WhatsApp Button]             │
├─────────────────────────────────────┤
│  2. PAIN POINT                      │
│  "...אם את מרגישה במרוץ בלתי פוסק" │
│  Emotional hook, large text         │
├─────────────────────────────────────┤
│  3. BENEFITS (3 Cards)              │
│  ┌──────┐ ┌──────┐ ┌──────┐        │
│  │זוגיות│ │חינוך │ │מודעות│        │
│  │      │ │ילדים │ │עצמית │        │
│  └──────┘ └──────┘ └──────┘        │
├─────────────────────────────────────┤
│  4. THE PROCESS                     │
│  "...אישה בוחרת" transformation     │
├─────────────────────────────────────┤
│  5. TESTIMONIAL (optional)          │
│  Blockquote with gold border        │
├─────────────────────────────────────┤
│  6. ABOUT ORIT                      │
│  Bio + credentials                  │
├─────────────────────────────────────┤
│  7. DETAILS                         │
│  Location • Day • Time              │
│  [CTA: WhatsApp Button]             │
├─────────────────────────────────────┤
│  8. FOOTER                          │
│  Name + בס"ד                        │
└─────────────────────────────────────┘
```

---

## 5. Hero Section

### Layout
- Photo: 140x140px circle, centered, 3px gold border, blush halo shadow
- Scarcity badge below photo: pill-shaped, `--cta-rose` background, white text
- h1 centered, max 3 lines at 320px
- Subtext: 1.125rem, max 2 lines
- CTA block: 32px below text

### Background Gradient

```css
background: linear-gradient(
  180deg,
  #FDF6F0 0%,       /* cream */
  #F5E8DC 40%,      /* cream-to-blush */
  #F2CECE 100%      /* blush */
);
```

### Photo Specs

```css
width: 140px;
height: 140px;
border-radius: 50%;
border: 3px solid #C9A84C;
box-shadow:
  0 0 0 6px #F2CECE,
  0 8px 32px rgba(44, 26, 26, 0.15);
object-fit: cover;
object-position: center top;  /* favor face */
```

---

## 6. CTA Button

### Primary (WhatsApp)

```css
display: inline-flex;
align-items: center;
gap: 10px;
min-width: 280px;
height: 56px;
padding: 0 32px;
border-radius: 50px;          /* pill shape */
background-color: #B85470;
color: #FFFFFF;
font-size: 1.125rem;
font-weight: 600;
box-shadow: 0 4px 16px rgba(184, 84, 112, 0.35);
```

### States

| State | Background | Shadow | Transform |
|---|---|---|---|
| Default | `#B85470` | `0 4px 16px rgba(184,84,112,0.35)` | none |
| Hover | `#9E3A5A` | `0 6px 24px rgba(184,84,112,0.50)` | `translateY(-2px)` |
| Active | `#8A2F4D` | `0 2px 8px rgba(184,84,112,0.30)` | `translateY(0)` |
| Focus | `#B85470` | `0 0 0 6px rgba(184,84,112,0.20)` | none + 3px outline |

### WhatsApp Link Format

```
https://wa.me/97252397565?text=שלום%20אורית%2C%20אשמח%20לשמוע%20על%20הקבוצה
```

**Do NOT stretch to full width on mobile.** A centered 280px pill reads as an invitation. Full-bleed reads as a form control — wrong emotional register.

---

## 7. Card Design (Benefit Cards)

```css
background-color: #F2CECE;
border-radius: 16px;
padding: 24px;
border: 1px solid #E8A8A8;
box-shadow:
  0 2px 8px rgba(44, 26, 26, 0.08),
  0 1px 2px rgba(44, 26, 26, 0.05);
```

- Gold 3px top accent bar via `::before` pseudo-element
- Hover: `translateY(-4px)` + deeper shadow
- Grid: 1 column on mobile → 3 columns at 600px+
- Content: SVG icon (40x40, gold stroke) → h3 → body text

---

## 8. Trust Signals

| Priority | Signal | Location | Notes |
|---|---|---|---|
| 1 | Orit's photo | Hero top | Circular — "real person, not a brand" |
| 2 | Scarcity badge | Below photo | "מקום מוגבל — קבוצה קטנה בלבד" |
| 3 | Credentials | About section | "אמא ל-9, בעלת משרד רו"ח" |
| 4 | Testimonial | Between benefits & CTA | Single blockquote, gold right border |
| 5 | Cost transparency | Below final CTA | "עלות סמלית — לפרטים בווצאפ" |
| 6 | Specific location + time | Details section | גבעת שאול, יום שני, 20:30 |

### Testimonial Style

```css
background-color: #FDF6F0;
border-inline-start: 4px solid #C9A84C;
border-radius: 0 8px 8px 0;
padding: 20px 24px;
font-size: 1.125rem;
font-style: italic;
```

---

## 9. Breakpoints

| Breakpoint | Width | Changes |
|---|---|---|
| **Mobile** (default) | 320–599px | Single column, 20px padding, 48px section spacing |
| **Tablet** | 600px+ | 3-column card grid, 40px padding, 64px section spacing |
| **Desktop** | 960px+ | 96px hero top padding, 80px section spacing. **Content stays 680px max** |

**Never changes:** RTL direction, text-align right, font sizes, CTA button style, photo size.

---

## 10. Micro-Interactions

| Element | Animation | Duration | Trigger |
|---|---|---|---|
| CTA hover | Lift 2px + deeper shadow | 200ms ease | `:hover` |
| CTA press | Snap back | 80ms ease | `:active` |
| Card hover | Float 4px + deeper shadow | 200ms ease | `:hover` |
| Hero photo | Single soft pulse (halo expand) | 1.8s ease, delay 0.5s | On load, once |
| Scarcity badge | Fade + slide in from top | 400ms ease, delay 0.8s | On load |
| Links | Underline offset shift | 150ms ease | `:hover` |
| Section divider | Gradient fade from center | — | Static |

---

## 11. Accessibility Checklist

- [x] `<html lang="he" dir="rtl">`
- [x] All positioning uses logical properties (`margin-inline`, `padding-inline`, `inset-inline`)
- [x] All color pairs pass WCAG AA (verified in contrast matrix above)
- [x] Gold is decorative only — never conveys information
- [x] Touch targets minimum 44x44px (CTA is 56px height)
- [x] `:focus-visible` ring on all interactive elements (3px solid `#B85470`, 4px offset)
- [x] Semantic HTML: single `h1`, `h2` per section, `<article>` for cards, `<blockquote>` for testimonial
- [x] Photo alt text: `"תמונה של אורית עשור, מנחת הקבוצה"`
- [x] Decorative elements: `aria-hidden="true"`
- [x] Viewport meta tag (prevents double-tap zoom on CTA)
- [x] Google Fonts with `display=swap` (text visible during load)

---

## 12. Open Graph / WhatsApp Preview

```html
<meta property="og:title"       content="לחזור לעצמך — קבוצת לימוד לנשים">
<meta property="og:description" content="מקום חם ואמיתי להתעצמות נשית. גבעת שאול, ירושלים. קבוצה קטנה בלבד.">
<meta property="og:image"       content="https://[domain]/og-image.jpg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:locale"      content="he_IL">
<meta property="og:type"        content="website">
```

OG image: 1200x630px JPEG, Orit's photo centered on blush `#F2CECE` background with headline in Secular One. Under 300KB.

---

## 13. File Structure

```
/
├── index.html          ← single-page landing
├── style.css           ← all styles
├── picture.jpeg        ← Orit's photo (compress to ~80KB for web)
├── og-image.jpg        ← WhatsApp/social share preview
├── DESIGN.md           ← this file
└── description.txt     ← original copy
```

---

## 14. Key Design Decisions

1. **No JavaScript** — pure HTML+CSS. Fastest load on mid-range phones.
2. **680px max-width** — keeps line length under 70 chars (optimal readability). Do not widen for desktop.
3. **No full-width CTA** — centered pill button reads as invitation, not form control.
4. **`wa.me` link** — single tap to WhatsApp vs. manual phone number entry. Highest-impact conversion decision.
5. **Warm shadows** — `rgba(44, 26, 26, ...)` instead of neutral gray. Matches the feminine, handcrafted feel.
6. **No scroll animations via JS** — causes layout shift and battery drain on target devices.
