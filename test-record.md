# Test Record — The Forgotten Handheld: Why the Game Boy Still Matters

L6 · Documentation and Testing

## Shape-wrap breakpoint test — PASS

Tested at 840px, 1087px, 1088px, and 1280px (1088px = 68rem at the default 16px root font size). Below 68rem, the Game Boy Advance figure remained in normal flow. At 1088px and above, the floated `shape-outside` treatment engaged and the opening paragraph followed the circular image boundary without colliding with the caption. The following paragraph cleared the complete figure, and the next section was unaffected.

## CSS-disabled reading-order test — PASS

Disabled `styles.css` and reviewed the page in the browser's default document flow at 1280px. The content remained in a logical source order: header and introduction → story guide → Built Around Limitations → From Gray to Color → The Advance Generation → Why We Still Play → L6 Documentation and Testing. Section headings remained associated with their content, images and captions remained in their appropriate sections, and the story-guide links remained available and usable. No content depended on CSS positioning for its meaning or reading order.

## 200% zoom and keyboard-focus test — PASS

Tested the page at 200% browser zoom. Content reflowed into the narrow layout without text overlap, clipping, or horizontal page overflow. The story-guide links remained keyboard accessible with clearly visible focus indicators. The pull quote also reflowed cleanly at 200%, remaining fully readable within its container without clipping or overlapping surrounding content.

## Content-growth stress test — PASS

Temporarily extended the main page title and doubled the content of a body paragraph at 1280px. The longer heading wrapped naturally and increased the height of the header without clipping or overlapping the badge, introduction, or following content. The doubled paragraph increased vertically and pushed the pull quote and subsequent content downward in normal document flow. No overlapping, clipping, or unintended horizontal overflow was observed.

## Sticky release test — PASS

At 1280px, scrolled through the story to the boundary between L5 and L6. The "In This Story" navigation remained sticky while moving through the story content, then released at the end of its containing story layout. It did not continue into or overlap the L6 Documentation and Testing section.

## Pointer interaction test — PASS

At 1280px, tested all four links in the "In This Story" navigation using pointer input. Each visible link remained clickable and navigated to its corresponding story section. No positioned, sticky, clipped, or overlapping element intercepted pointer interaction.

## `clip-path` fallback — PASS

Disabled the enhanced `clip-path` declaration in DevTools at 1280px. The feature image reverted to its underlying rectangular presentation while remaining fully visible within the figure. The caption and surrounding content remained readable, with no overlap, clipping, or loss of information.

## `shape-outside` fallback — PASS

Disabled `shape-outside` in DevTools at 1280px while leaving the figure's float enabled. The opening paragraph fell back to normal rectangular float wrapping beside the Game Boy Advance figure. The figure, caption, opening paragraph, and following content remained readable with no overlap or loss of information.

## Stacking-context inspection — PASS

Inspected the positioned elements in Chrome DevTools. The pull quote computed to `position: relative` with `z-index: 10` from `var(--layer-raised)`, while the `.story-guide` computed to `position: sticky` with `z-index: 20` from `var(--layer-sticky)`. The absolutely positioned issue badge had no explicit `z-index`. This confirmed the intended layer hierarchy, with the sticky navigation above raised content, and no unintended stacking or overlap problems were observed.

### HTML Validation

**Result:** PASS

**Validator:** Nu Html Checker (vnu 26.9.16)

Final HTML validation completed with:
- 0 errors
- 0 warnings

The earlier article-heading warning was resolved by adding an accessible visually hidden heading to the article.

### CSS Validation

**Result:** PASS with documented validator limitation

**Validator:** Nu Html Checker / CSS validation

**Findings:**
The validator reported three errors:
- `shape-outside` reported twice as an unknown property
- `shape-margin` reported once as an unknown property

These properties are intentionally used for the L5 CSS Shapes requirement. They are placed inside an `@supports` feature query so browsers that support CSS Shapes receive the enhanced layout, while unsupported browsers retain the normal fallback layout.

The fallback was also manually tested in Chrome DevTools by disabling the `shape-outside` declaration. Content remained readable and usable without the shaped text wrapping.

No changes were made solely to remove these validator messages because doing so would remove the CSS Shapes enhancement required by the assignment.