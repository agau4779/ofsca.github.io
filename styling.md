# OFSCA Site Style Guide

How text, colour and timelines look on oakland-fukuoka.org, and where each rule lives.

## Where styles live

| File | Owns |
| --- | --- |
| `assets/css/site.css` | Google Sites layout and components (nav, header, grid). Font stacks point at `var(--font-sans)`. |
| `assets/css/theme.css` | Section colours (white, pale-green and dark-green bands, photo hero), spacing, and the `.sN` utility classes from the original export. **It has no font families or sizes.** |
| `assets/css/typography.css` | **The source of truth.** Design tokens, the type scale, heading hierarchy, link styles and timelines. It loads last on every page. |

Each page `<head>` loads the fonts from Google Fonts, then `site.css`, `theme.css` and `typography.css`, in that order.

## Typefaces

| Role | Family | Token | Weights used |
| --- | --- | --- | --- |
| Everything (body, headings, nav, buttons) | **Plus Jakarta Sans** | `--font-sans` | 400, 500, 600, 700, 800 (+ italic) |
| Timelines only | **Space Grotesk** | `--font-timeline` | 400–700 |

Plus Jakarta Sans is a contemporary geometric sans with open, friendly shapes. It stays readable at body sizes and still has character in bold display titles.
Space Grotesk has a squarer, more technical feel and clear figures, so dates read as data and timeline entries stand apart from the prose around them.
Both are loaded as variable fonts with `display=swap`. Each falls back to the system UI font.

Do not add other families. Pasted text that arrives with an inline `font-family` should be stripped (see “Pasting content” below).

## Type scale

The sizes scale fluidly with the viewport between phone and desktop widths, so no per-breakpoint overrides are needed.

| Level | Applies to | Token | Size (mobile → desktop) | Weight | Colour |
| --- | --- | --- | --- | --- | --- |
| Display | Page title band (`.LB7kq`), banner titles (`.gk8rDe`) | `--fs-display` | 36 → 52px | 800, −0.025em tracking | white on photo / brand green |
| H1 | Section headings (`h1.duRjpb`) | `--fs-h1` | 28 → 36px | 700 | `--color-brand` |
| H2 | Sub-sections (`h2.JYVBee`) | `--fs-h2` | 22 → 26px | 700 | `--color-brand` |
| H3 | Minor headings (`h3.OmQG5e`) | `--fs-h3` | 18 → 20px | 600 | `--color-brand` |
| Body | Paragraphs and list items (`.zfr3Q`) | `--fs-body` | 17px | 400, line-height 1.65 | `--color-text` |
| Small | Captions (`.TMjjoe`) | `--fs-small` | 14px | 400 | `--color-muted` |
| Nav / buttons | Side nav (`.PsKE7e`), buttons (`.QmpIrf`) | `--fs-nav` | 15px | 500 / 600 | theme |
| Site name | Header and sidebar “OFSCA” | `--fs-brand` / `--fs-h2` | 20px / 26px | 700 | `--color-accent` / `--color-brand` |

Rules:

- **One heading per level of meaning.** Don't use a bigger heading to make something stand out. Use the next level down for anything nested under it.
- Headings ignore font weight from pasted spans: `.duRjpb span` etc. inherit the heading weight.
- Body text has a single size. To emphasise something, use **bold** (700) or `--color-alert`. Don't change the size.
- Headings use `text-wrap: balance` so titles that wrap don't leave a single word on the last line.

## Colour

| Token | Value | Use |
| --- | --- | --- |
| `--color-text` | `#212121` | Body copy |
| `--color-muted` | `#5f6368` | Captions, secondary nav |
| `--color-brand` | `#617e4d` | Headings |
| `--color-brand-dark` | `#4f694d` | Headings on pale bands, timeline dates |
| `--color-accent` | `#8bbb67` | Decorative rules under titles, focus rings |
| `--color-surface-dark` | `#637457` | Dark-green bands, primary buttons |
| `--color-surface-tint` | `#eef3e5` | Pale-green bands |
| `--color-on-dark-accent` | `#fcfbdf` | Headings and links on dark bands |
| `--color-alert` | `#b3261e` | Deadlines, “rain or shine” notices, other warnings |
| `--color-link` / `--color-link-hover` | `#3f6b2f` / `#2a4a1f` | Links (see below) |
| `--color-sakura*` | pink / rose / gold | Timeline flower only |

Earlier one-off colours (pure black, near-blacks, navy, and the Google-Docs link blues) were removed so the text inherits `--color-text`. Pasted greens map to `--color-brand` or `--color-brand-dark`, and the three different reds map to `--color-alert`. White text on dark bands and the yellow announcement bar were left unchanged.

## Links

Every content link (`a.XqQF9c`, and in-page jump links `a.aw5Odc.mD9Vkc`) looks the same on every page:

- Colour `--color-link`, with a 1px underline at 45% opacity offset 0.2em below the text.
- On hover: darker `--color-link-hover` and a solid 2px underline.
- On keyboard focus: a 2px `--color-accent` outline.
- On dark-green or photo bands (`.lQAHbd`, `.O13XJf`, `.cJgDec`), links turn cream (`--color-on-dark-accent`) and white on hover.
- Any colour or underline on spans inside a link is ignored, so pasted blue or underlined spans can't produce double underlines or a different colour.

Buttons (`.QmpIrf`) are not links for styling purposes. They keep the filled or outlined button look from `theme.css`.

## Timelines

Pages with a timeline: **History** (past presidents), **Calendar** (yearly events), **Torii Gate** (restoration history), **Otsukimi** (evening schedule) and **Mural Fabrication** (session dates).

Timelines are set in **Space Grotesk**. Each entry has a **sakura flower bullet**: five notched pink petals with a gold centre, inlined as an SVG data URI in `typography.css`, so there is no extra request. The date or time is pulled out into `.tl-date`. It is semibold, uses tabular figures, and is coloured `--color-brand-dark`.

Two markup patterns:

```html
<!-- 1. A list of short dated entries (Calendar) -->
<ul class="n8H08c UVNKR tl">
  <li class="zfr3Q TYR86d">
    <p class="zfr3Q"><span class="tl-date">January 19</span><span>MLK Day of Service…</span></p>
  </li>
</ul>

<!-- 2. Flat entries with optional details (History, Torii Gate, Otsukimi, Mural) -->
<h3 class="tl-item zfr3Q OmQG5e"><span class="tl-date">1962 – 1963</span><span>Homer Bemis</span></h3>
<p class="tl-body zfr3Q">Biography…</p>

<p class="tl-item zfr3Q"><span class="tl-date">5:30pm</span><span>Bonsai Garden &amp; Bento Dinner</span></p>
<ul class="tl-body n8H08c">…</ul>
```

- In `.tl` lists the date sits in a fixed 8.5em column and wrapped text hangs beside it. Below 480px the date stacks above the text.
- In `h3.tl-item` the date is followed by a small accent-green “·” separator before the name.
- `.tl-body` indents supporting paragraphs and lists to line up with the entry text. They stay in the body font (Plus Jakarta Sans) so long biographies remain comfortable to read.
- Write date ranges with an en dash and spaces (`1962 – 1963`). Write time ranges without spaces (`2–5 pm`).

To add an entry, copy an existing one and keep the classes. To start a new timeline on another page, use one of the two patterns above. No extra CSS is needed.

## Pasting content from Google Docs / Sites

Pasted text often brings inline `font-family`, `font-size`, `line-height` and colour styles. These were all removed from the existing pages. When you add content:

1. Remove `style="font-family:…; font-size:…; line-height:…; color:…"` from the pasted spans and paragraphs.
2. Keep only meaningful emphasis: `font-weight: 700`, `font-style: italic`, `color: var(--color-alert)` for warnings.
3. Use a real `h1/h2/h3` with the matching class (`duRjpb`, `JYVBee`, `OmQG5e`) for headings. Don't use a large bold paragraph instead.
