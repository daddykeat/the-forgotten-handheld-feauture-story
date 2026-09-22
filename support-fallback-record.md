# Support and Fallback Record

## The Forgotten Handheld: Why the Game Boy Still Matters

**Research date:** September 22, 2026

This record documents the enhanced CSS features used in the project, why
they are used, how the page behaves when an enhancement is unavailable or
disengaged, and the references consulted during implementation.

The project follows a progressive-enhancement approach. The story remains
readable in normal document flow before positioned, layered, clipped, or
shape-wrapped treatments are applied.

---

## 1. CSS Positioning

### Where it is used

CSS positioning is used for several intentional relationships:

- The feature header uses `position: relative` as the containing block for
  the generation badge.
- The generation badge uses `position: absolute` at wider viewports.
- The story guide uses `position: sticky` in the two-column layout.
- The pull quote uses `position: relative` so its overlap can participate in
  the project's controlled layer system.
- A decorative header pseudo-element uses absolute positioning.

### Purpose

Positioning is used only where an element needs a deliberate spatial
relationship with another element.

The generation badge is anchored to the feature header rather than to the
viewport. The sticky story guide remains available while the reader moves
through the article. The pull quote creates a controlled editorial overlap
at wider widths.

### Baseline / fallback

The important content begins in normal document flow.

At narrow widths:

- the generation badge remains in normal flow;
- the story guide remains a normal navigation block;
- the pull quote remains inside the article column without overlap.

This prevents the positioned relationships from becoming necessary for
reading or navigating the story.

### Support research

MDN documents `position` and the `static`, `relative`, `absolute`, `fixed`,
and `sticky` positioning values. It also explains that an absolutely
positioned element is removed from normal flow and positioned relative to
its closest positioned ancestor when one exists.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position

**Accessed:** September 22, 2026

---

## 2. Sticky Positioning

### Where it is used

At the 52rem layout breakpoint, the story guide uses `position: sticky`
with a block-start offset.

### Purpose

The sticky treatment keeps the four story-section links available while the
reader scrolls through the longer article.

The sticky behavior is tied to the wider two-column composition because that
layout provides a dedicated navigation column. Sticky positioning is not
needed when the guide and article are stacked vertically.

### Baseline / fallback

Below 52rem, the story guide remains in normal document flow above the
article and does not use sticky positioning.

If sticky positioning does not behave as expected, the guide still exists in
the document at its original source location and all four navigation links
remain available.

### Support research

MDN documents `sticky` as a value of the `position` property. A sticky
element behaves according to its scrolling container and offset values while
remaining constrained by its containing layout.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position

**Accessed:** September 22, 2026

---

## 3. z-index and the Layer System

### Where it is used

The project uses a small tokenized layer scale:

- `--layer-base`
- `--layer-raised`
- `--layer-sticky`

The overlapping pull quote uses the raised layer, while the interactive
sticky story guide uses the higher sticky layer.

### Purpose

The layer system resolves the intentional overlap between the pull quote and
the story guide.

The navigation receives the higher layer because its links must remain
visible and interactive even when the pull quote extends toward the guide's
column.

The generation badge does not receive a custom `z-index` because no competing
element overlaps it. Additional layer values were not added when the
composition did not require them.

### Baseline / fallback

Without the enhanced overlap, the pull quote and story guide remain readable
in normal flow.

The layer system is therefore used to resolve an intentional visual
relationship rather than to make content accessible.

Purely decorative positioned content also uses `pointer-events: none` where
appropriate so it cannot intercept interaction with meaningful content.

### Support research

MDN documents `z-index` as controlling the z-order of positioned elements
and their descendants, with larger stack levels appearing above smaller
ones within the relevant stacking context.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/z-index

Additional MDN guidance on stacking:

https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Positioned_layout/Using_z-index

**Accessed:** September 22, 2026

---

## 4. border-radius

### Where it is used

`border-radius` is used on components such as the story guide and other
card-like or badge-like treatments.

### Purpose

Rounded corners visually group interface-like elements while providing
contrast with the sharper, pixel-inspired media treatment.

### Baseline / fallback

The components remain complete rectangular boxes if `border-radius` is
unsupported or disabled.

No story content, navigation, or functionality depends on rounded corners.

### Support research

MDN documents `border-radius` as the CSS property used to round the corners
of an element's outer border edge.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/border-radius

**Accessed:** September 22, 2026

---

## 5. clip-path

### Where it is used

`clip-path: polygon()` is used on the primary feature image.

### Purpose

The polygon removes small portions of the image corners to create a
restrained pixel-inspired silhouette that supports the Game Boy visual
theme.

The treatment changes the visible silhouette of the image rather than the
layout or reading order.

### Baseline / fallback

The feature image begins as a complete responsive rectangle.

The `clip-path` enhancement is placed inside an `@supports` feature query. If
the tested clipping feature is unavailable, the rule is not applied and the
complete rectangular image remains visible.

The caption and surrounding story content remain outside the clipping
treatment.

### Support research

MDN documents `clip-path` as creating a clipping region that determines what
portion of an element is displayed.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/clip-path

**Accessed:** September 22, 2026

---

## 6. @supports Feature Queries

### Where it is used

`@supports` feature queries conditionally apply enhancements including:

- the `clip-path` image treatment;
- the circular `shape-outside` treatment.

### Purpose

Feature queries allow the page to establish a usable baseline first and then
apply an enhancement only when the browser recognizes the tested CSS
declaration.

### Baseline / fallback

If a tested feature is unavailable:

- the clipped feature image remains rectangular;
- the Game Boy Advance media uses its float fallback without the custom
  circular wrapping boundary;
- story content, captions, and reading order remain available.

The feature queries therefore enhance an already usable composition rather
than gating content behind feature support.

### Support research

MDN documents `@supports` as a CSS feature query that applies a block of CSS
when a browser supports a specified CSS feature.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@supports

**Accessed:** September 22, 2026

---

## 7. shape-outside

### Where it is used

At 68rem and wider, the Game Boy Advance `<figure>` floats
`inline-start`.

The figure uses a shared length-valued custom property for its media size:

`--portrait-size`

That value controls the figure width and is also used to calculate the
radius and center of the circular `shape-outside` treatment.

### Purpose

The circular shape creates a genuine editorial text wrap around the round
Game Boy Advance artwork instead of forcing the opening paragraph to follow
the rectangular boundary of the floated figure.

The complete `<figure>` is the floated element because the image and caption
need to remain one semantic media unit.

However, the figure is taller than the square image because it also contains
the caption. A percentage-based circle would therefore calculate its geometry
from a reference box whose height includes that caption.

To avoid allowing caption height to distort the circle, the final
implementation derives the circle's radius and center from half of the
length-valued `--portrait-size`. The resulting shape corresponds to the
square image region at the top of the taller floated figure.

### Why the enhancement begins at 68rem

The page's primary two-column layout begins at 52rem, but testing showed that
the shaped media treatment required more horizontal space than the grid
itself.

When the float and circular wrap were enabled near the 52rem breakpoint, the
remaining prose column became excessively narrow and competed visually with
the image and caption.

The shaped treatment therefore remains disengaged until 68rem.

This creates three responsive states:

1. Below 52rem — single-column layout, static story guide, and normal-flow
   Game Boy Advance figure.
2. From 52rem to below 68rem — two-column layout and sticky story guide, but
   the Game Boy Advance figure remains in normal flow.
3. At 68rem and wider — two-column layout, sticky story guide, floated Game
   Boy Advance figure, and circular text wrap.

These breakpoints control different relationships and do not need to engage
at the same width.

### Float containment and clearing

The Game Boy Advance section uses `display: flow-root` to contain the floated
figure so the float cannot affect the following story section.

The opening paragraph is allowed to wrap around the circular shape.

The following paragraph uses `clear: inline-start` so it begins below the
complete floated figure, including its caption. This prevents article prose
from entering the caption area.

### Baseline / fallback

Below 68rem, the figure remains in normal document flow and no
`shape-outside` treatment is applied.

At 68rem and wider, if `shape-outside` is unavailable, the figure can still
function as an ordinary rectangular float. The image, caption, article
content, and reading order remain available.

The shaped wrap is therefore an enhancement rather than a requirement for
understanding the story.

### Verified responsive test

**PASS:** Tested at 840px, 1087px, 1088px, and 1280px
(1088px = 68rem at the default 16px root font size).

Below 68rem, the Game Boy Advance figure remained in normal flow. At 1088px
and above, the floated `shape-outside` treatment engaged and the opening
paragraph followed the circular image boundary without colliding with the
caption.

The following paragraph cleared the complete figure, and the next section
was unaffected.

### Support research

MDN documents `shape-outside` as defining a shape around which adjacent
inline content wraps. It supports basic shapes including `circle()`,
`ellipse()`, `inset()`, and `polygon()`.

MDN also documents that `circle()` accepts a radius and an optional position
for the center of the circle.

**MDN — shape-outside:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/shape-outside

**MDN — Basic shapes with shape-outside:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Shapes/Using_shape-outside

**Accessed:** September 22, 2026

---

## 8. shape-margin

### Where it is used

`shape-margin` is paired with the circular Game Boy Advance
`shape-outside` enhancement.

### Purpose

The shape margin adds breathing room between the circular wrapping boundary
and the surrounding article text.

This spacing is calculated around the CSS shape rather than functioning as a
normal box margin.

### Baseline / fallback

The figure already uses ordinary margins as part of its floated layout.

If `shape-margin` or the shape enhancement is unavailable, readable spacing
does not depend exclusively on the shape margin.

Below 68rem, the complete shaped-media treatment disengages and the figure
returns to normal flow.

### Support research

MDN documents `shape-margin` as setting a margin around a CSS shape created
with `shape-outside`, increasing the distance between the shape and
surrounding content.

**MDN:**  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/shape-margin

**Accessed:** September 22, 2026

---

## Progressive Enhancement Summary

The page begins with semantic HTML, a logical source order, and a usable
normal-flow layout.

Enhancements are added only when they improve the composition without making
content dependent on them.

The enhancement path is:

1. Semantic HTML and normal document flow.
2. A two-column composition at 52rem.
3. Anchored and sticky positioned relationships at appropriate widths.
4. A minimal tokenized layer system for the intentional pull-quote/navigation
   overlap.
5. Decorative rounding that does not affect content.
6. `clip-path` enhancement with a complete rectangular-image fallback.
7. A normal-flow Game Boy Advance figure below 68rem.
8. A floated Game Boy Advance figure at 68rem and wider.
9. A circular `shape-outside` and `shape-margin` enhancement when supported.
10. Explicit clearing and float containment so captions and following content
    cannot collide with the shaped media.

No essential story content, navigation, caption, link, or control depends on
positioning, clipping, layering, shape wrapping, or decorative generated
content.