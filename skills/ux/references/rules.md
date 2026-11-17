# The UX rules

The numbered rules that 21 Grams UX audits every flow against. They're written for mobile-first products and apply to the web too: "bottom tab" means the primary nav, and "bottom sheet" means a sheet on touch and a popover or small dialog on desktop.

Each entry has the rule, how to apply it through the project's own components, and what to flag in an audit. The area files in `rules/` say where each rule belongs.

---

## 1–5

> Awaiting the author's source.

---

## 6. X closes, the left arrow goes back
**Rule:** An X closes a modal or flow. A left arrow goes back one screen.
**Apply:** Modals, sheets and full-screen flows started from elsewhere get an X that returns to where the person came from, with the flow's state discarded or saved as a draft (#12). Pushed screens inside a stack get a back arrow that pops exactly one level. Never use both on the same screen, and never an arrow that dismisses a whole flow. Use the project's existing header or navigation bar component and its icon set.
**Flag:** An X that goes back one step, a back arrow that closes everything, a modal with no close, back and close side by side.

## 7. Never a blank screen while loading
**Rule:** Never show a blank screen while content loads. Use a skeleton, spinner or progress bar.
**Apply:** Skeletons for content with a known layout (lists, feeds, cards, profiles), shaped like the real content so nothing jumps when it arrives. A spinner for short waits with unknown shape. A progress bar for anything measurable (uploads, imports, multi-step jobs). Put the state in the shared data or list component, so every screen gets it. Keep the page chrome (header, nav) on screen while the content loads.
**Flag:** White or empty screens during fetches, layout shift when content arrives, full-page spinners that hide the nav, skeletons that don't match the real layout.

## 8. Keep the scroll position
**Rule:** When people leave a feed and come back, they return to their exact scroll position.
**Apply:** Going into a detail and back restores the list where it was, with the same items loaded. Use the router's scroll restoration or keep the list mounted (cached query plus stored offset) rather than refetching from the top. Paginated feeds keep the pages that were already loaded.
**Flag:** Back from a detail lands at the top, a refetch that reorders or reloads the list, infinite lists that drop loaded pages on return.

## 9. Tap the active tab to go to the top
**Rule:** Tapping the bottom tab that's already selected returns people to the top of that tab.
**Apply:** First tap on the active tab pops its stack to the root; a tap at the root scrolls to the top (smoothly, unless reduced motion is on). Wire it in the project's tab or nav component, once, for every tab.
**Flag:** Tapping the active tab does nothing, or reloads the tab and loses state.

## 10. Load the next batch before the end
**Rule:** Feeds load the next batch of content before people reach the bottom.
**Apply:** Start fetching the next page when the person is roughly one screen (or a few items) from the end, with an intersection observer or the list library's threshold. Show a small inline loader only if they outrun it, and an inline retry if the fetch fails. Say clearly when they've reached the end.
**Flag:** Fetching only at the very bottom, a "Load more" button on a feed, a blocking spinner between pages, no end-of-feed message, a failed page that silently stops the feed.

## 11. Optimistic likes, follows and saves
**Rule:** Likes, follows and saves update immediately, then sync in the background.
**Apply:** Change the UI on tap (state, count, icon), send the request in the background, and on failure roll back and say so with a short message and a retry. Debounce rapid toggles so the last state wins. Use the data layer's optimistic-update support if it has one.
**Flag:** Toggles that wait for the server, spinners inside like buttons, counts that jump after a delay, failures that leave the UI out of sync with no message.

## 12. Save drafts automatically
**Rule:** Save drafts and unfinished input automatically, so going back doesn't erase them.
**Apply:** Persist form and composer input as people type (debounced) to the project's store, local storage or a server draft. Restore it when they return, and clear it on submit. If something genuinely can't be kept, warn before leaving rather than losing it silently.
**Flag:** Back, close or a refresh that wipes typed input, long forms with no draft, drafts that never clear after sending.

## 13. Ask for permissions in context
**Rule:** Ask for notifications, photos, camera or location only when people try to use the related feature.
**Apply:** No permission prompts at launch or during onboarding. Trigger the system prompt from the action that needs it (tap "Add photo", then ask for photos), optionally preceded by one line saying why. If it's denied, keep the feature reachable and explain how to turn it on in settings.
**Flag:** Prompts on first launch, several prompts in a row, prompts with no visible reason, dead ends after a denial.

## 14. Quick actions in a bottom sheet
**Rule:** Quick actions open in a bottom sheet, and swiping down dismisses it.
**Apply:** Short action lists (share, edit, report, move) open in the project's sheet component, anchored to the bottom on touch, with a grabber, swipe-down to dismiss, tap-outside and Escape to close. On desktop, the same actions open in a popover or menu at the trigger. Keep full forms and long flows out of sheets.
**Flag:** Quick actions as full-screen pages or centred modals on mobile, sheets that can't be swiped away, sheets with no close on desktop.

## 15. Links open the exact content
**Rule:** Notifications and shared links open the exact content they reference, not the home screen.
**Apply:** Every notification and shareable item has a route that renders it directly, with a back stack that makes sense (back from a deep-linked post goes to its parent, then home). If sign-in is required, sign in and then continue to the content. If the content is gone, say so on that route and offer the nearest useful place.
**Flag:** Links and notifications that land on home, a sign-in that forgets where the link was going, a broken route for deleted content, deep links with no back path.

---

## Quick audit checklist

| # | Area | Check |
|---|---|---|
| 6 | Navigation | X closes the flow, arrow goes back one screen |
| 7 | States | Skeleton, spinner or progress, never blank |
| 8 | Navigation | Scroll position restored on return |
| 9 | Navigation | Active tab tap goes to top |
| 10 | States | Next page prefetched before the end |
| 11 | Feedback | Optimistic toggles, rollback on failure |
| 12 | Forms | Drafts saved and restored |
| 13 | Onboarding | Permissions asked in context |
| 14 | Navigation | Quick actions in a dismissible sheet |
| 15 | Navigation | Links and notifications open the exact content |
