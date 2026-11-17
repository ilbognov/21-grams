# 20 ways to unslop AI designs

Adapted from the short video "20 Ways to Unslop AI Designs" (credited in the README).
These are the composition and content tells of AI-built pages: what's on the page and how it's weighted, not just how it's styled. Each entry has the rule, the before/after from the video, how to apply it, and what to flag. Where an entry repeats a rule 21 Grams UI already has, it points there instead.

---

### 1. Delete filler badges
**Rule:** Remove decorative "NEW" / "Beta" / announcement pills that don't help the reader do anything.
**Demo:** A hero "Agents that survive production." Before: a `NEW · Evals as deploy gates are now GA →` pill above the headline. After: the headline stands alone.
**Apply:** Keep a badge only when it carries real, current information the user can act on (a status, a count, a date-bound launch the page is about). One per view at most.
**Flag:** Pills above hero headlines, "NEW" on things that aren't, badge stacks.

### 2. Drop redundant labels
**Rule:** Don't label what the content already says.
**Demo:** An FAQ section. Before: a tiny "FAQ" eyebrow above "Questions, answered." After: no eyebrow.
**Apply:** Remove eyebrows, section labels and captions that repeat the heading. An eyebrow earns its place only when it adds context the heading doesn't (a category, a step number in a real sequence).
**Flag:** Uppercase eyebrows that restate the heading; "Features" above a features grid.

### 3. Un-italicise random words
**Rule:** Don't italicise or recolour a random word in a headline for flair.
**Demo:** "Small studio. *Wide-open* thinking." Before: one phrase in an italic serif. After: set in the same roman style.
**Apply:** Use italics for their real jobs (titles of works, foreign terms, true emphasis in running text). Headlines carry emphasis through wording and weight, not a style switch on one word.
**Flag:** One italic or gradient word inside an otherwise upright headline.

### 4. Mono only where needed
**Rule:** Monospace is for code, commands and copyable hashes or keys, not for flavour, labels or numbers.
**Demo:** "An engineer that lives in your `terminal`▌". Before: the last word in a mono font with a blinking cursor. After: the same sans as the headline, in the accent colour.
**Apply:** Keep mono only in code blocks, inline code, CLI snippets and copyable hashes or keys. Remove it from headlines, labels, eyebrows, badges, buttons, timestamps, IDs and figures; aligned numbers use `tabular-nums` in the sans. The strict rule is in `rules/type.md`.
**Flag:** Mono words in headlines, fake terminal cursors, mono used as "techy" decoration.

### 5. Use a design system
**Rule:** Controls in one toolbar come from one system.
**Demo:** A dashboard toolbar. Before: a segmented range picker, a blue outlined "Simulate signup" and a white filled "Export CSV", three button styles side by side. After: one consistent set.
**Apply:** This is rule zero (SKILL.md): use the project's components and their variants. Siblings share size, radius and style; one primary at most (see #10).
**Flag:** Neighbouring buttons in different styles, sizes or radii.

### 6. Show the actual product
**Rule:** Show the real product, not abstract decoration.
**Demo:** "Curiosity, meet clarity." Before: a glossy 3D blue sphere with floating chips. After: a real answer card from the product, with the question, answer and cited sources.
**Apply:** Replace stock 3D blobs, orbs, gradients and abstract illustrations with real UI (a screenshot, a live component, a real example output). If the product isn't ready, show the closest real artefact.
**Flag:** Hero art that could belong to any product.

### 7. Enlarge the main feature
**Rule:** Features aren't equal, so don't lay them out as equal.
**Demo:** Three equal feature cards. After: the main feature ("Ship without the setup.") takes a large cell with a bigger heading; the other two sit smaller beside it.
**Apply:** Pick the one feature that matters most and give it more space, a bigger heading or a visual. The rest support it.
**Flag:** Rows of identical feature cards with identical icons and three-line blurbs.

### 8. Group with spacing
**Rule:** Let whitespace do the grouping, not lines and boxes.
**Demo:** A dark 2×2 feature grid. Before: hairline dividers between every cell and cramped padding. After: no dividers, more space between items than within them.
**Apply:** See `rules/spacing.md` (tighter inside groups than between) and `rules/elevation.md` (no box around everything).
**Flag:** Dividers and borders doing the job spacing should do.

### 9. Make headlines specific
**Rule:** Say what the product does, concretely.
**Demo:** Before: "Curiosity, meet clarity." After: "Cited answers from papers."
**Apply:** A headline should name the outcome or the mechanism. Avoid the "X, meet Y." pattern, abstract nouns ("clarity", "possibility", "the future of"), and lines that could sit on any landing page.
**Flag:** Headlines you could swap onto a competitor's site unchanged.

### 10. Emphasise the CTA
**Rule:** One call to action is the primary; the rest step back.
**Demo:** Pricing. Before: both "Start 14-day trial" buttons are strong (purple on Pro, solid black on Business). After: Pro keeps the filled accent button; Business gets an outlined one.
**Apply:** See `rules/buttons.md` (one primary per view). In pricing, the recommended plan gets the filled button.
**Flag:** Several filled buttons competing in one view.

### 11. Add an accent colour
**Rule:** The primary action carries the accent, not neutral black.
**Demo:** A bio form. Before: "Save changes" in black, the same weight as everything else. After: "Save changes" in the brand accent (orange).
**Apply:** See `rules/colour.md`: one accent, used for the primary action, focus and selection. Check text contrast on the accent (AA).
**Flag:** A primary action that looks like every other dark element; accent spread across decoration instead.

### 12. Keep icons consistent
**Rule:** One icon style and one library; no emoji as icons.
**Demo:** Habit tiles. Before: emoji (water drop, book, runner, meditating person) in circles. After: matching line icons in the accent colour.
**Apply:** See `rules/icons.md`.
**Flag:** Emoji icons; mixed icon styles.

### 13. Remove embellishments
**Rule:** Drop glows, gradient borders and other decoration that adds no meaning.
**Demo:** A "Most popular" pricing card. Before: a glowing purple-to-pink gradient border. After: a plain card; the badge and the filled CTA already mark it.
**Apply:** Mark emphasis once (a badge or a filled button), not three ways at once.
**Flag:** Glow shadows, gradient borders, animated sheens, decorative blurs.

### 14. Inner radius = outer − padding
See `references/design-hacks.md` #1 and `rules/radius.md`.

### 15. Improve text contrast
**Rule:** Secondary text still has to be readable.
**Demo:** A manifesto paragraph. Before: one sentence in pale grey ("We can measure what they do, but rarely why."). After: the same sentence at body contrast.
**Apply:** See `rules/type.md` and `rules/colour.md`: body text ≥ 4.5:1. Show emphasis with weight or wording, not by fading a sentence.
**Flag:** Pale grey sentences mid-paragraph, light-grey body copy.

### 16. Wrap headlines properly
**Rule:** No orphans, and no awkward breaks inside a highlighted phrase.
**Demo:** "Simple pricing that scales with / you". Before: "you" alone on the second line. After: "Simple pricing that / scales with you", balanced and with the highlighted phrase kept together.
**Apply:** `text-wrap: balance` on headings (see `rules/type.md`); keep highlighted phrases on one line (`white-space: nowrap` on the span, or a manual break).
**Flag:** One-word last lines in headlines; highlighted phrases split across lines.

### 17. Align by eye, not by pixels
**Rule:** Round and pointed shapes need optical alignment; geometric alignment looks wrong.
**Demo:** A "See it in action" play button. Before: the circle box aligns to the text's left edge, so the round edge looks indented. The play triangle also sits geometrically centred, which looks too far left. After: the circle is nudged out so its visual edge lines up, and the triangle is shifted right so it looks centred.
**Apply:** Overshoot round shapes slightly past the edge; shift play triangles right ~6–10% of their width; align icons to the text's cap height, not its line box.
**Flag:** Circles that look inset next to text; play icons that look off-centre.

### 18. Use tabular numbers
**Rule:** Changing or aligned numbers use tabular figures so they don't jitter.
**Demo:** A live revenue counter ($42,870.11 → $42,863.55). Before: digits shift width as they change. After: `font-variant-numeric: tabular-nums`, steady.
**Apply:** See `rules/type.md`. Use them for counters, timers, prices that update, and table columns. Large static hero numbers can stay proportional.
**Flag:** Jittering counters; misaligned number columns.

### 19. Add loading states
**Rule:** Never show an empty frame while data loads.
**Demo:** A "Recent transactions" table. Before: empty rows under the headers. After: the rows fill in, with a skeleton that matches the final row layout while loading.
**Apply:** Skeletons shaped like the real content (same row height and columns); keep the frame and headers; show progress past 400ms (`references/principles.md` #17). Distinguish loading from a true empty state.
**Flag:** Blank tables and cards while fetching; spinners that replace the whole layout.

### 20. Animate useful feedback
**Rule:** Animate the moments that confirm an action, not decoration.
**Demo:** "ADD TO CART" becomes "ADDED ✓" on click.
**Apply:** See `references/animation-craft.md` #8, #16 and #18: overlap old and new labels, blurred icon swap, one success wave. Keep the button width stable.
**Flag:** Actions with no visible confirmation; decorative motion that confirms nothing.

---

## Quick audit checklist

| # | Check | Pass when |
|---|---|---|
| 1 | Badges | only real, actionable information |
| 2 | Labels and eyebrows | none that repeat the heading |
| 3 | Headline styling | no random italic or recoloured word |
| 4 | Monospace | only code, commands, copyable hashes/keys; never labels or numbers |
| 5 | Toolbars and button rows | one system, one style |
| 6 | Hero visual | the real product, not abstract art |
| 7 | Feature layout | the main feature is bigger |
| 8 | Grouping | spacing, not dividers |
| 9 | Headlines | specific outcome or mechanism |
| 10 | CTAs | one filled primary per view |
| 11 | Accent | on the primary action, AA contrast |
| 12 | Icons | one style, no emoji |
| 13 | Decoration | no glows or gradient borders |
| 14 | Nested radius | inner = outer − padding |
| 15 | Text contrast | body ≥ 4.5:1, no faded sentences |
| 16 | Headline wrap | balanced, no orphans, phrases intact |
| 17 | Optical alignment | circles and play icons look aligned |
| 18 | Changing numbers | tabular figures |
| 19 | Loading | skeletons in the final layout |
| 20 | Feedback | confirmation is animated, nothing else is |
