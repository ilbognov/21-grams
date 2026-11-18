# UX research step

Before auditing or redesigning a flow, 21 Grams UX looks at how the best products in the same space solve it. The rules say what good looks like in general. Research shows what good looks like for this kind of product, this audience and this flow.

Run it at the start of every new flow, redesign or onboarding, and whenever the person asks "how do others do this?".

## 1. Start from where the person is

Ask, or work out from the code and the conversation:
- **What's being designed:** the product, its category (banking, learning, B2B tool, marketplace…) and its platform (iOS, Android, web, desktop).
- **Which flow:** onboarding, sign-up, checkout, search, settings, an empty state…
- **Who it's for,** and what they're trying to get done in that flow.
- **What exists today:** a live build, a prototype, a Figma file, or nothing yet.

## 2. Analyse the product being redesigned

If there's something to look at, walk its flow first (in the browser, simulator or designs) and write down:
- every step from entry to the end state, with a screenshot of each;
- what each step asks of the person (decisions, typing, waiting);
- where it breaks the laws (`laws.md`), rules (`rules.md`) and field rules (`field-rules.md`).

This becomes the "before" that the research is compared against.

## 3. Recommend industry-leading examples

Always recommend that the person looks at similar products before designing. Pick three to five leaders:
- **Same category first** (another bank for a bank), then **best in class for the flow** from any category (a famously good onboarding, whatever the product).
- **Use a pattern library when one is connected.** With Mobbin, search flows by flow and category ("banking app onboarding", "onboarding") on the right platform, and use the screens it returns. Don't describe screens you haven't seen.
- **Without a library,** name well-known leaders, link their sites or App Store pages, and ask the person to walk the flows or share screenshots.

Give a one-line reason for each pick, so the person can swap any of them.

## 4. Analyse the examples one at a time

Go through the examples one by one with the person, not all at once. For each:
- **The flow:** the steps in order, with the step count.
- **What it does well:** each pattern, with the UX law or rule behind it (A1–A7, #n, Fn) and why it works for this audience.
- **What to avoid:** dark patterns, friction that only suits that business.
- **What it means for our product:** the patterns worth borrowing, adapted to the project's own components (rule zero).

Cite each example with its source link (Mobbin URL, site or App Store page). Wait for the person's take before moving to the next one.

## 5. Bring it together

After the last example:
- **Compare:** a table of patterns across the examples and today's flow (who does what).
- **Recommend:** the changes for this product, ranked by impact, each linked to the examples that support it.
- **Agree, then build:** the person picks what to adopt; the normal audit and fix workflow (SKILL.md) takes it from there.

Patterns that hold across several leaders and that the person adopts become field rules (`field-rules.md`), so the next project starts from them.
