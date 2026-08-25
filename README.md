# Chat-first intake — live prototype

A self-contained, clickable prototype of the flow in `../chat-first-intake-spec.md`,
now covering **three flows as three tabs** (top bar). No build step, no backend — the
agent is scripted, all data is mock (fictional brand "Cardevra"; client persona Priya
Sharma at Meridian Therapeutics; CEL persona Maya Chen). Visual language is lifted from
Solstice-Frontend's editorial register (`app/globals.css` + `DESIGN.md` at `fe2226ad`).

## Run it

Either double-click `index.html`, or (nicer URLs):

```
cd docs/specs/intake-chat-redesign/prototype && python3 -m http.server 4173
# → http://localhost:4173
```

Aileron is bundled in `fonts/`; Spectral loads from Google Fonts (falls back to Georgia offline).

**Round-3 changes:** the "I assumed" block is gone — assumed values are now ordinary
receipt rows carrying an ember `assumed` tag (italic value); correcting one converts it
to stated and the mark disappears. Banners are multi-size: toggle chips + a "Build these
N →" commit, one Sizes row on the receipt, and a per-size gallery on the asset canvas.
The empty composer teaches: a ghost brief types itself (stops the moment you type;
static under reduced-motion) and three example-brief cards below attach their source
file when tapped. The tab-1 confirmation now composes in a single choreographed
entrance (stamped REQ number → record → timeline inking → one heartbeat of the mark)
and then goes completely still — the "In production" dot is static ember, never
breathing, so nothing reads as watchable progress.

**Round-4 changes** (spec: `../2026-08-24-round4-spec.md`): the ghost typing is gone —
the composer placeholder now teaches the brief anatomy ("What is it, who's it for, and
what should we build from?") and the example cards sit under a "From recent Cardevra
work" caption. File purposes: unset renders as an ember `use: my call ▾` on the attach
card; the menu is two intents (Match its design / Use its content → as-is / as
inspiration); "Let the agent decide" and "both" are gone (typing still works); a
purpose set on the card suppresses the clarify question; the Built-from row always
names the purpose with provenance. The tab-1 confirmation collapsed: record shows as
its header strip + "View the full record ▾" (expanded on the days-later record page),
the sub line and timeline caption are cut, and the voice line carries the merged
handoff + 24–48h turnaround.

## Tab 1 — Client intake, hands off to a CEL

Same intake as the end-to-end flow (chips, receipt, tap-to-edit) but the receipt button
reads **Submit request →** and the client never sees a build. On submit the chat collapses
(same gesture as everywhere) and the space fills with the confirmation: the receipt reborn
as the request record, stamped with a request number, plus a **handoff timeline in the
stage rail's anatomy** (Submitted → In production → Back to you), who has it (Maya Chen),
and the honest wait (24–48h). The composer stays live — typed notes ride along to the CEL.
From there: **View my requests** (a status home with client-vocabulary statuses:
In production / Back to you / Delivered — never internal pipeline states), request records
for the days after, and for a returned request, **Review the asset** with feedback routed
to the CEL, not self-serve editing.

## Tab 2 — CEL picks up a client request

Opens on the review queue (dashboard → review page → workspace collapsed to
**queue → one surface that is the workspace**). Clicking a "V1 ready" row lands on the
asset + a dock with a Request/Chat toggle. The Request panel is the pinned receipt grown
into the CEL's fidelity object:

- **"Does V1 match the ask?"** — every captured input pre-checked against V1 with
  evidence; hover a row to see the region glow on the asset, click to scroll to it.
  The one mismatch (client assumed *no CTA*; V1 has one) is flagged in ember with
  **Remove the button** (drops into the chat editor: propose → keep → V2, flag flips ✓)
  or **Keep it — note to client**.
- Request info (requester, submitted, brand, project, type, job code, status),
  original prompt verbatim, clarifications from Q&A, references with purposes —
  the same fields as the current admin review page (`admin-review-request-page.tsx`).
- Toolbar: versions, Upload source / Upload final asset (mock), **Send to client →**
  (guards if a fidelity flag is still open; marks the request Back to you).

**Continuity:** a request submitted on Tab 1 appears in this queue ("generates" for ~15s,
then V1 ready) — and its "Back to you" status shows on the client's requests home.

## Tab 3 — CEL end-to-end

The original full flow, unchanged: brief → clarify → receipt → **Create it** → build
canvas → asset → iterate. Edge cases (one-word brief, wall-of-text, build failure) intact.

## ✳ Demo menu (bottom right)

Restart this tab · Client: skip to submitted confirmation · CEL scenarios (one-word brief,
pasted client brief, failing build, skip to finished asset). Build time is compressed ~16×.
Switching tabs restarts that tab's flow; the shared request ledger persists across tabs
within a session.
