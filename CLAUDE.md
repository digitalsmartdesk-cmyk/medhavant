# Medhavant — notes for Claude Code

This is Vikas Gupta's one-page marketing site for Medhavant, a business
transformation consulting practice. Read `README.md` first for full
context on structure, status, and open items before changing anything.

## Hard constraints

Do not relax any of these without the owner (Vikas) explicitly asking:

- Never invent testimonials, client names, "founding clients," case
  studies, or quantified results (rupee/dollar figures, percentages).
  Every illustrative example already in the file says, in its own
  copy, that it's illustrative — keep that pattern for anything new.
- Never state a fee or fee range.
- Never add stock photography or AI-generated imagery. Use only assets
  from `brand-assets/`.
- Never reintroduce internal launch-tactics language — event
  registration mechanics, attendee counts, roadmap targets, specific
  city targeting (e.g. Vadodara). These were deliberately stripped out
  of the public site; they live only in the owner's internal strategy
  doc.
- Keep all text at WCAG AA contrast or better. The brand's bright gold
  (`#c08920`) fails AA on white/light backgrounds for normal text —
  use `--gold-text` (`#8a6217`) there instead.
- Keep it a single self-contained HTML file (inline CSS, minimal
  vanilla JS, base64-embedded images, zero external requests) unless
  told otherwise.
- Don't add a backend or a third-party form-relay service (Formspree,
  FormSubmit, etc.) to the enquiry form without the owner explicitly
  asking for it — the current form intentionally stays client-side
  only (builds a `mailto:` link). See README's "Known limitation"
  section before touching `#enquiry-form` or its script.
- Don't deploy or publish this anywhere public without explicit
  sign-off — it's a draft pending review.
- No LinkedIn link anywhere on the page — removed at the owner's
  request; don't re-add it without being asked.

## Before changing copy

Check `docs/paragraphs.txt` and `docs/tables.txt` (the strategy
document extraction) for the offer architecture (Clinic/on-site sprint
→ Diagnostic → Pilot → Monthly partnership), the four capabilities, and
segment/pain language. That document is the authoritative source —
don't paraphrase from a guess at what the brief said.

## Good next task if asked to improve this

The enquiry form's "did the mail app open?" detection is a
`window.blur` heuristic with a 1.2s timeout — not reliable on every
browser/OS combination. If asked to harden it, test across a few real
browsers rather than just headless Chromium, and keep the fallback
message focused on getting the visitor to email
`medhavant@growthoriginator.in` directly (their typed input isn't
currently preserved into that fallback — consider whether to show it
back to them to copy, without over-engineering a backend-free page).
