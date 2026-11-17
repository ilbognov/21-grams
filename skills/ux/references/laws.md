# The UX laws

The laws behind the rules: the essential knowledge 21 Grams UX reasons from when no specific rule covers a case. Laws are cited by section and number (A1, A2…), so they never clash with the numbered rules in `rules.md` (#1, #2…).

21 Grams UI applies some of the same laws at component level (target size, choices in one menu, response time). 21 Grams UX applies them across a whole flow: how many decisions a task asks for, how far the next step is, where complexity lands.

Each entry has the law, where it applies, how to apply it in an existing product, and what to flag in an audit.

---

## A. Core UX laws

### A1. Hick's Law
**Law:** The more choices people have, the longer it takes them to decide.
**Applies to:** Navigation, menus, onboarding, filters, pricing pages and forms.
**Apply:** Cut the choices at each step to what that step needs. Lead with a recommended or default option, put the common few first and disclose the rest ("More filters", "Advanced"). Split a long decision into a few smaller ones in sequence. Keep top-level navigation short and grouped.
**Flag:** Menus and navs with a long flat list, filter panels that show everything at once, pricing with more than three or four plans and no recommendation, onboarding that asks for every preference up front, several equal-weight primary actions.

### A2. Fitts's Law
**Law:** The time to reach a target depends on its size and its distance.
**Applies to:** Buttons, navigation, touch targets, primary actions and mobile interfaces.
**Apply:** Make the primary action large and close to where the person's attention or thumb already is (the bottom of the screen on mobile, next to the content it acts on). Hit areas are at least 44×44 on touch, even when the icon is smaller. Keep destructive actions small and away from the primary. Use screen edges and corners for frequent targets on desktop.
**Flag:** Primary actions in a far corner of a long screen, small tap targets packed together, a primary next to a destructive action, the main mobile action out of thumb reach at the top.

### A3. Jakob's Law
**Law:** People spend most of their time in other products, so they expect familiar patterns.
**Applies to:** Navigation, search, shopping carts, authentication and SaaS conventions.
**Apply:** Use the standard placement, icon and behaviour unless there's a real reason not to: logo top-left goes home, search at the top with a magnifier, cart or account top-right, settings under the avatar, sign-in with the usual fields, password managers and passkeys working. Follow the platform's conventions (iOS, Android, web) for back, sheets and tabs.
**Flag:** Novel navigation for a common job, renamed standard things ("Vault" for settings), custom sign-in that breaks autofill, search hidden behind an unfamiliar icon, platform conventions broken without a reason.

### A4. Miller's Law
**Law:** Working memory is limited. Grouping information into meaningful chunks makes it easier to process.
**Applies to:** Forms, dashboards, onboarding, settings and complex information.
**Apply:** Group related fields and settings under clear headings, keep each group short, and order groups the way people think about the task. Chunk long numbers and codes. Don't make people remember something from one screen to use on the next: show it again or carry it forward.
**Flag:** Long ungrouped forms, settings pages as one flat list, dashboards with every metric at the same weight, flows that ask people to recall a code or value from an earlier step.

### A5. Doherty Threshold
**Law:** Responsive interactions keep people engaged. The commonly cited 400ms is a useful historical benchmark, not a universal cutoff.
**Applies to:** Loading states, search, feedback, transitions and asynchronous actions.
**Apply:** Acknowledge every input straight away (pressed state, optimistic update, inline spinner), then show progress for anything that takes noticeably longer. Make search feel live with debounced results. Prefetch the likely next step. Treat 400ms as a prompt to check, not a pass mark: what matters is that people are never left wondering whether something happened.
**Flag:** Taps with no visible response, saves that block the UI, search that only runs on Enter when live results are expected, long waits with no progress, slow transitions between steps.

### A6. Tesler's Law
**Law:** Every system has complexity that can't be removed. Good design manages it instead of pushing it all onto the people using it.
**Applies to:** Complex workflows, enterprise software, configuration and automation.
**Apply:** Let the product carry the complexity: sensible defaults, values inferred from what's already known, smart pre-fill, templates, automation for repeated steps. Keep advanced control available for the people who need it, behind progressive disclosure, rather than removing it.
**Flag:** Configuration that asks for things the system already knows, blank setups with no defaults or templates, every option exposed to every user, "simplified" flows that removed control experts need with no way to get it back.

### A7. Postel's Law
**Law:** Be conservative in what you send and liberal in what you accept.
**Applies to:** Input fields, formatting, data imports and user-generated content. Apply carefully where security and data integrity matter.
**Apply:** Accept the formats people actually type (spaces and dashes in phone and card numbers, any date format the locale allows, pasted values with stray whitespace) and echo back one clean, normalised value. Imports tolerate column order and common variants and report what they changed. Be strict where it counts: validate and sanitise on the server, never loosen authentication, permissions or money fields to be "forgiving", and confirm rather than guess when an input is ambiguous.
**Flag:** Fields that reject valid input because of formatting, imports that fail on one odd row with no report, silent guesses on ambiguous values, leniency that weakens security or data integrity.

---

## Quick audit checklist

| Law | Area | Check |
|---|---|---|
| A1 Hick's | Choice | Few choices per step, a recommended default, the rest disclosed |
| A2 Fitts's | Accessibility | Primary large and close, 44×44 touch, destructive kept apart |
| A3 Jakob's | Navigation | Standard placement, icons and platform conventions |
| A4 Miller's | Choice | Grouped and chunked, nothing to remember between steps |
| A5 Doherty | Feedback | Instant acknowledgement, progress for longer waits |
| A6 Tesler's | Flows | Product carries the complexity, defaults and templates, advanced disclosed |
| A7 Postel's | Forms | Forgiving input, clean echo, strict on security and integrity |
