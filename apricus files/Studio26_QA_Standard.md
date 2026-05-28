# Studio26 QA Standard
## Required for All Builds — Claude Code Enforcement Block

This section is mandatory on every Studio26 project. Do not skip or abbreviate any item. Run the full checklist after all feature tasks are complete, before confirming done.

The three pillars are: **Functional QA**, **Mobile Responsiveness**, and **WCAG 2.1 AA Accessibility Compliance**.

---

## Pillar 1 — Functional QA

### Forms
- Every required field must show a clear inline error if submitted empty. Error text must be adjacent to the field, not just a page-level alert.
- Optional fields must never block submission.
- Success state must be visually distinct from the form (not just a console log).
- No form should silently fail. If submission has no backend, confirm the client-side success state is unambiguous.
- Ensure no field accepts XSS payloads without sanitisation (strip or encode `<`, `>`, `"`, `'`, `&` from any displayed output).

### Navigation
- Every anchor link must resolve. No `href="#"` on visible navigation items unless it is an intentional placeholder, in which case it must have a `title` or `aria-label` explaining the state.
- Back-button behaviour must not break the page state.
- If a hash route or modal is used (e.g. `#privacy`), the browser back button must close it cleanly.

### Images
- Every image must have a meaningful `alt` attribute. Decorative images must have `alt=""` and `role="presentation"`.
- No broken image paths. Verify every `src` resolves on the deployed URL, not just localhost.
- Images must not overflow their containers at any viewport width.

### Console
- Zero console errors on load and on all user interactions.
- Zero 404s in the network tab for any asset (fonts, images, scripts, stylesheets).

### Cross-browser baseline
- Verify layout renders correctly in Chrome, Firefox, and Safari (mental model check if live browser not available). Flag any CSS that is known to behave differently across these three.

---

## Pillar 2 — Mobile Responsiveness

### Viewport and Breakpoints
- The page must have `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
- Test mentally at: 375px (iPhone SE), 390px (iPhone 14), 430px (iPhone 14 Plus), 768px (iPad), 1024px (iPad landscape / small laptop), 1440px (desktop).
- No horizontal scroll must appear at any of these widths. If it does, find the overflow source and fix it (common causes: fixed-width elements, uncontrolled flex children, wide images without `max-width: 100%`).

### Touch Targets
- Every interactive element (buttons, links, inputs, dropdowns) must have a minimum tap target of **44x44px** per Apple HIG and WCAG 2.5.5.
- Links that are inline in body text are exempt but must be clearly underlined.
- Navigation items must not be so close together that adjacent taps are ambiguous.

### Typography at Mobile
- No font size below 14px on mobile. Body text should be at minimum 16px.
- Line length should not exceed 75 characters on any viewport (use `max-width` on text containers).
- Headings must reflow gracefully — no truncation, no overflow, no text clipping.

### Layout at Mobile
- Multi-column grid layouts must stack to single column at or below 640px unless the columns are narrow enough to be readable side-by-side.
- Tables that are too wide for mobile must either scroll horizontally with `overflow-x: auto` on a wrapper, or reflow into a card/list format.
- Fixed or sticky elements must not eat more than 15% of the screen height on mobile.

### Forms at Mobile
- Input fields must be full width on mobile.
- Dropdowns must be native `<select>` elements or have a touch-friendly replacement.
- The submit button must be at minimum 44px tall and full-width or prominent on mobile.
- Ensure `autocomplete` attributes are set on standard fields: `given-name`, `family-name`, `email`, `organization`, `country` where applicable.

---

## Pillar 3 — WCAG 2.1 AA Compliance

### Colour Contrast
- Normal text (below 18pt / 24px regular, or 14pt / 18.67px bold): minimum contrast ratio **4.5:1** against background.
- Large text (18pt+ regular or 14pt+ bold): minimum contrast ratio **3:1**.
- UI components and graphical objects (icons, input borders, focus rings): minimum **3:1** against adjacent colour.
- Check every text/background combination in the design, including: body on page background, headings on section backgrounds, text on coloured cards, placeholder text in inputs, label text on buttons, badge/tag text on badge backgrounds.
- Use the contrast formula mentally or reference: [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).
- If a colour combination fails, adjust the darker or lighter value until it passes. Do not reduce font size as a workaround.

### Keyboard Navigation
- Every interactive element must be reachable and operable by Tab key alone.
- Tab order must follow the visual reading order (top to bottom, left to right). Do not use `tabindex` values above 0 unless there is a documented reason.
- No keyboard trap: the user must always be able to Tab out of any component (modals, dropdowns, forms).
- Dropdown menus and modals opened by keyboard must be closable by Escape key.

### Focus Indicators
- Every focusable element must have a visible focus ring. Do not use `outline: none` or `outline: 0` without providing an equivalent custom focus style.
- The focus indicator must meet **3:1** contrast against the surrounding background.
- Acceptable: `outline: 2px solid #005fcc; outline-offset: 2px;` or equivalent in the site's colour system.

### Semantic HTML
- Page must have exactly one `<h1>`. Heading hierarchy must be logical: `h1` > `h2` > `h3`. No skipped levels (e.g. `h1` directly to `h3`).
- Navigation must use `<nav>` with an `aria-label` if there are multiple nav regions (e.g. `aria-label="Main navigation"`, `aria-label="Footer navigation"`).
- The main content area must be wrapped in `<main>` with `id="main-content"` for the skip link.
- Lists of items must use `<ul>` or `<ol>`, not `<div>` or `<p>` with bullet characters.
- Buttons that trigger actions must be `<button>` elements, not `<div>` or `<span>` with click handlers.
- Links that navigate must be `<a href="...">` elements, not `<button>` or `<div>`.

### Skip Link
- A "Skip to main content" link must be the first focusable element in the DOM.
- It may be visually hidden until focused (`position: absolute; left: -9999px` then `left: 0` on `:focus`).
- It must link to `#main-content` and that ID must exist on the `<main>` element.

### Forms and Labels
- Every form input must have an associated `<label>` with a matching `for` / `id` pair. Placeholder text alone is not a label.
- Required fields must be indicated both visually and programmatically: use `aria-required="true"` or `required` attribute, and a visible indicator (asterisk is acceptable if explained at the top of the form: "Fields marked * are required").
- Error messages must be linked to their input via `aria-describedby`.
- The form success or error state must be announced to screen readers: use `role="alert"` or `aria-live="polite"` on the response container.

### Images and Icons
- Informative images: `alt` text must describe the content and purpose, not just the file name.
- Decorative images: `alt=""` and optionally `role="presentation"` or `aria-hidden="true"`.
- Icon-only buttons must have `aria-label` describing the action (e.g. `<button aria-label="Close menu">`).
- SVG icons used inline must have `aria-hidden="true"` if accompanied by visible text, or `role="img"` and a `<title>` if they convey meaning alone.

### Colour Independence
- Information must never be conveyed by colour alone. Any use of colour to indicate state (error, success, required) must also use a text label, icon, or pattern.
- Example: a red border on an invalid field is acceptable only if accompanied by visible error text.

### Motion and Animation
- Any animation that loops or auto-plays must respect `prefers-reduced-motion`. Wrap animations in:
  ```css
  @media (prefers-reduced-motion: no-preference) {
    /* animation here */
  }
  ```
- Do not use flashing content that flashes more than 3 times per second.

### Language
- The `<html>` element must have a `lang` attribute: `<html lang="en">`.
- If sections of the page are in a different language (e.g. French phrases), wrap them in a `<span lang="fr">` or equivalent.

---

## QA Sign-Off Checklist

Run through every item before marking a build complete. Check each as you go.

### Functional
- [ ] All forms validate required fields inline
- [ ] Form success state is visually confirmed
- [ ] All navigation anchors resolve correctly
- [ ] Hash routes / modals close cleanly on back button and Escape
- [ ] All image `src` paths resolve on the deployed URL
- [ ] Zero console errors on load and on all interactions
- [ ] Zero 404s in network tab

### Mobile
- [ ] No horizontal scroll at 375px, 390px, 430px, 768px
- [ ] All tap targets minimum 44x44px
- [ ] No font below 14px on mobile (body text minimum 16px)
- [ ] Multi-column layouts stack correctly below 640px
- [ ] Tables have overflow-x scroll wrapper or reflow
- [ ] Form inputs are full width on mobile
- [ ] Submit button is prominent and minimum 44px tall on mobile
- [ ] `autocomplete` attributes set on standard fields

### WCAG 2.1 AA
- [ ] All normal text meets 4.5:1 contrast ratio
- [ ] All large text meets 3:1 contrast ratio
- [ ] All UI components meet 3:1 contrast ratio
- [ ] Every interactive element reachable by Tab
- [ ] Tab order follows visual reading order
- [ ] No keyboard traps
- [ ] Escape closes modals and dropdowns
- [ ] Visible focus ring on all focusable elements, meeting 3:1 contrast
- [ ] Exactly one `<h1>`, heading hierarchy logical and unbroken
- [ ] `<nav>` elements have `aria-label`
- [ ] `<main id="main-content">` present
- [ ] Lists use `<ul>` / `<ol>`, not div-based bullets
- [ ] Buttons are `<button>`, links are `<a href>`
- [ ] Skip link present and functional as first focusable element
- [ ] Every input has a `<label for="...">` (not placeholder-only)
- [ ] Required fields marked with `aria-required="true"` or `required`
- [ ] Error messages linked via `aria-describedby`
- [ ] Form response container has `role="alert"` or `aria-live="polite"`
- [ ] Decorative images have `alt=""`
- [ ] Informative images have descriptive `alt` text
- [ ] Icon-only buttons have `aria-label`
- [ ] Colour is never the sole indicator of state
- [ ] Animations wrapped in `prefers-reduced-motion` media query
- [ ] `<html lang="en">` present

---

*Studio26 QA Standard v1.0 — applies to all client builds.*  
*Governs: Cloudflare Workers, static sites, React apps, and any other frontend deliverable.*  
*Review and version this document when WCAG 3.0 reaches Candidate Recommendation.*
