# Medhavant Website — Handoff

Vikas Gupta's one-page marketing site for **Medhavant**, a business
transformation consulting practice serving owner-run manufacturing,
trading and service businesses across India.

## Status

**Draft. Not live.** This has not yet been approved to replace any
public-facing site. Do not deploy it anywhere public until the owner
(Vikas) explicitly says to.

## What this is

A single, self-contained HTML file: `site/index.html`. No build step,
no framework, no backend, no external network requests. All CSS is
inline in one `<style>` block. The only JavaScript is: the mobile nav
toggle, the collapsible "program library" disclosure, and the enquiry
form handler described below. The logo, favicon and apple-touch-icon
are embedded as base64 data URIs directly in the HTML.

**Preview it** by opening `site/index.html` in a browser, or serving
the folder: `cd site && python3 -m http.server`.

## Page structure (section ids, in order)

- `#hero` — proposition + single CTA (scrolls to `#contact`) + a "what a number card looks like" template visual
- `#issues` — the business pressures the firm addresses (prose, no cards)
- `#approach` — the four capabilities (See clearly → Steer daily → Grow → Govern) as a connected sequence
- `#start` — three generic "starting point" categories, plus a collapsible full program library
- `#how` — engagement path: Clinic/on-site sprint → Diagnostic → Pilot → Monthly partnership
- `#about` — Vikas Gupta's verified credentials only
- `#trust` — data handling and human-review commitments
- `#contact` — the enquiry form, the plain-text email, and the footer

## Design tokens

Defined as CSS variables at the top of the `<style>` block:
`--navy`, `--navy-deep`, `--gold`, `--gold-text`, `--teal`, `--white`,
`--bg-grey`, `--text-body`, `--text-muted`, `--rule`, `--max-w`, `--measure`.

**Important:** the raw brand gold (`#c08920`) only reaches **3.07:1**
contrast on white — it fails WCAG AA (4.5:1) for normal-size text.
`--gold-text` (`#8a6217`, ~5.1–5.5:1 on white/pale-grey) was derived to
pass AA and is used for all small text on light backgrounds. The
brighter `--gold` is reserved for rules, borders, large/bold text, and
text on dark navy backgrounds. Verify any new color pairing's contrast
before shipping it.

## The enquiry form (`#contact`)

There is no backend. The form (`#enquiry-form`) collects name, type of
business, a reply contact (email or phone), and the issue, then on
submit builds a `mailto:` link from those values (subject + body) and
sets `window.location.href` to it — handing off to whatever mail app
is configured on the visitor's device.

Because the page can't actually detect whether a mail app opened, the
script uses a heuristic: it listens for a `window` `blur` event for
1.2 seconds after redirecting. If the window never loses focus in that
window (likely meaning no mail app took over), the note under the
submit button (`#enquiry-note`) switches to telling the visitor to
email `medhavant@growthoriginator.in` directly. This is a best-effort
fallback, not a guarantee — see "Known limitation" below.

## What's real vs. illustrative

- The hero "number card" shows the **format only** — no finding, real
  or invented, is displayed. The text explicitly says a real result
  would replace it.
- The three `#start` examples are generic "starting file → kind of
  output" patterns, labeled as a category of problem, not a record of
  any client's actual data or results.
- `#about` contains only verified facts: IIM Ahmedabad, AI
  governance/advisory work, and two live links — `author.vikasgupta.world`
  ("Read More") and `aitrilogy.vikasgupta.world` ("The AI Trilogy")
  (both confirmed reachable).
- There are no testimonials, client names, "founding clients," case
  studies, or quantified outcomes anywhere on the page. This is
  deliberate — see Hard Constraints in `CLAUDE.md`.
- No LinkedIn link on the page (removed at the owner's request,
  2026-11-20).

## Open items (owner to confirm or supply — do not guess)

1. A real anonymised finding to eventually replace the generic
   number-card template, once one exists and the client has given
   permission to show it.
2. Real example scenarios to replace or supplement the three generic
   `#start` categories, once real engagements exist.
3. Contact email (`medhavant@growthoriginator.in`) — confirmed live by
   the owner (2026-11-20). All form submissions and mailto links point
   here.
4. Fees — intentionally unpublished anywhere on the site.
5. Naming decision (firm-name-first "Medhavant" vs. Vikas-Gupta-first)
   — currently firm-name-first. The owner's strategy document flags
   this as still undecided.

## Known limitation — the enquiry form still depends on a mail app

The form is a real form with real fields now, but under the hood it's
still a `mailto:` hand-off: nothing is actually transmitted until the
visitor's own mail app sends it. On a device or browser with no
default mail client configured (common on locked-down office machines,
some in-app browsers, or phones with no mail app signed in), the
fallback note will fire, but the visitor still has to copy the address
and write the note themselves — their original input isn't carried
over automatically.

**If the owner wants true "fill the form, it just arrives" delivery**
(no dependency on the visitor's own mail app), that requires either:
- a small backend endpoint that receives the POST and sends the email
  server-side, or
- a third-party form-relay service (e.g. Formspree, FormSubmit) that
  accepts the POST and forwards it to `medhavant@growthoriginator.in`.

Either is a real architecture change — it introduces a server or a
third party that the enquiry data passes through before reaching the
owner, which is a step beyond the current single-static-file, zero-
dependency approach. **Do not add this unprompted** — confirm with the
owner first, since it's adjacent to the data-handling promises made in
`#trust`, even though that section is about client business data, not
contact-form submissions.

## Contents of this handoff

- `site/index.html` — the current draft.
- `brand-assets/` — original logo files from the owner's `Brand_Assets.zip`,
  for reference if higher-resolution exports are ever needed.
- `docs/paragraphs.txt`, `docs/tables.txt` — full extraction of the
  owner's strategy document. This is the **authoritative source** for
  the offer architecture, the four capabilities, and segment/pain
  language — check it before rewriting any factual claim about what
  the firm does.
- `screenshots/` — latest reviewed desktop and mobile renders
  (top-of-page and full scroll), reflecting the enquiry form and
  trimmed About section.

## Rules this project has followed — keep following them

- No stock photography or AI-generated imagery anywhere — only the
  supplied brand logo.
- No invented testimonials, client names, "founding clients," case
  studies, or quantified results. Anything illustrative says so
  explicitly in its own copy.
- No fees stated anywhere.
- None of the owner's internal launch-tactics language (event
  registration mechanics, attendee counts, roadmap targets, specific
  city/geo targeting) appears on the public page.
- WCAG AA minimum contrast for all text.
- Single self-contained HTML file, unless the owner explicitly asks for
  a build step, a backend, or multiple files.

See `CLAUDE.md` for the same rules phrased as constraints for an
automated coding session.
