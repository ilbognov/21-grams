# 8g · Copy: plain and helpful

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Rules
- **Empty states** say what's empty and what to do next: "No teammates yet. Invite people by email. They only get access to this project."
- **Buttons** are a verb + object that say exactly what happens: "Invite people", "Send invoices", "Save changes". The confirmation echoes the verb: "Invite sent", "Saved".
- **Errors** say what failed, why if known, and how to fix it: "Couldn't send the invite to sam@acme.co. That address bounced, so check it and try again." Name the field. How errors look and behave is in `forms.md`.
- **Destructive confirms** name the thing and the consequence: "Delete 'Q3 roadmap'? This removes it for everyone."
- Sentence case. No exclamation marks. Use "you"/"your", not "my".
- Name things the way users know them ("notifications"), not the way the system is built ("webhook config").
- **No internal labels on screen.** Version tags ("V7", "v2.3 beta", "UX V7 demo"), build or draft names, ticket numbers and regulatory or engineering shorthand ("SaMD", "MVP", "feature flag") stay in code comments and the tab title. If a demo needs saying, say it plainly ("Demo", "Sample data").
- **One form of address.** Match the product's existing voice (informal or formal "you", and in languages that distinguish them, e.g. "ti/vi", "du/Sie", "tu/vous"); never switch within a product.
- Numbers and dates are formatted for reading: "Thursday, 15 January", "£48,210", chunked IDs.

## Banned
Emoji in UI text, "Oops!", "Something went wrong" with nothing after it, "Unlock", "Supercharge", "Seamless", "Effortless", "Amazing", "Elevate", "Get started" when something more specific exists, "Submit", "Click here", marketing-style subheads in product UI.
