# The Forgotten Handheld: Why the Game Boy Still Matters

## Project Overview

This project is a responsive editorial webpage about the Nintendo Game Boy and how its limitations helped shape its identity and long-term appeal.

The page follows the Game Boy through three generations: the original Game Boy, Game Boy Color, and Game Boy Advance. The project focuses not only on the content, but also on using CSS layout, positioning, layering, shapes, responsive behavior, and progressive enhancement in a way that keeps the page accessible and usable.

## Layout and Design

The page uses several layout techniques throughout the article:

- Normal document flow for the main article structure
- A sticky "In This Story" navigation guide on larger screens
- Positioned elements and intentional overlapping relationships
- Controlled `z-index` values for layered content
- CSS Shapes using `shape-outside`
- `clip-path` for enhanced image presentation
- Responsive layouts that return to simpler document flow on smaller screens
- Feature queries with `@supports` to provide progressive enhancement and fallback behavior

The visual design uses a limited color palette inspired by the Game Boy era, with blue, gray, and green accents.

## Accessibility

Accessibility was considered throughout the project.

The page includes:

- Semantic HTML landmarks and section structure
- Descriptive image alternative text
- Figure captions and image credits
- Visible keyboard focus states
- Keyboard-accessible navigation links
- A visually hidden article heading for accessible document structure
- Responsive layouts that remain readable at narrow viewport widths
- Fallback layouts when enhanced CSS features are unavailable

The page was also tested using keyboard navigation and browser accessibility tools.

## Progressive Enhancement and Fallbacks

CSS Shapes and clipping effects are treated as enhancements rather than requirements for accessing the content.

`@supports` feature queries are used so supported browsers receive the enhanced layouts. When properties such as `shape-outside` or `clip-path` are unavailable or disabled, the content returns to a conventional layout while remaining readable and usable.

The fallback states were manually inspected using Chrome DevTools.

## Testing

The project was manually tested for:

- Keyboard navigation
- Pointer/click interaction
- Responsive layouts
- Narrow viewport behavior
- Zoom and content reflow
- Sticky positioning
- Layering and stacking order
- CSS Shapes fallback behavior
- `clip-path` fallback behavior
- Link accessibility
- Image alternative text and captions

### HTML Validation

The final HTML was tested with the Nu Html Checker.

**Result:** 0 errors and 0 warnings.

### CSS Validation

The CSS was also checked with the Nu validation tool.

The validator reported `shape-outside` and `shape-margin` as unknown properties. These properties are intentionally used for the project's CSS Shapes requirement and are protected with progressive-enhancement/fallback techniques.

They were retained because removing them solely to satisfy the validator would remove an intentional part of the project.

## Media Credits

The project uses photographs of the original Game Boy, Game Boy Color, and Game Boy Advance.

Image attribution and source information are provided with the corresponding figures and in the project's media/source documentation.

## Project Documentation

Additional documentation includes:

- Composition Plan
- Support and Fallback Record
- Test Record
- Media Credits

These records document the design decisions, browser-support strategy, fallback behavior, accessibility testing, and final validation of the project.

## Technologies Used

- HTML5
- CSS3
- Responsive Web Design
- CSS Grid
- Flexbox
- CSS Positioning
- CSS Custom Properties
- CSS Shapes
- `clip-path`
- `@supports` feature queries
- Chrome DevTools
- Nu Html Checker

## Author

Keaton Moore