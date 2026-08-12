# Issue Log

Real production mistakes and fixes. **Newest first.** Don't delete old entries — mark them outdated if a fix stops working, but keep the history. Chronological order, latest first.

---

## 2026-08-12 — Log: Discovered Higgsfield's official face-consistency tool

Discovered `higgsfield-soul-id` — an official Higgsfield AI skill that automates face consistency for characters. Instead of manually re-uploading/re-describing a character's face every time (current method), it trains one reusable face ID and lets me reuse it instantly across future generations.

**Where this helps:** big projects with lots of characters — it would save serious time there.

**Why not now:** current workload doesn't need it. I can do the manual method myself; it takes more time but is safer (the automated tool's install process carries a minor security tradeoff — see toolkit doc for details).

**Decision:** parked, not installed. Logging it here as a known option for later — if a large-cast project comes up (e.g. manga-style production), revisit and install then.

---

## 2026-08-11 — Temple/bell scene: character "flies in like Superman" instead of impact

**Project:** OVERDRIVE
**What went wrong:** Prompt described the character "slamming into" the bell/piping. Instead of a physical hit, she flew in unhit, then landed — no impact rendered.
**Root cause:** Seedance can't reliably animate a named impact action described step-by-step. Confirmed hard rule: describe force + result, not the collision mechanics.
**Fix:** Rewrite as aftermath — e.g. "she is down near the bell, impact damage visible, dust settling" — instead of "slams into."
**Trials wasted before fix found:** 6–7

## 2026-08-11 — Briefing room: character enters from wrong side

**Project:** OVERDRIVE
**What went wrong:** Room has a projector on one side, door + map on the other. Character was supposed to enter through the door, but repeatedly entered through the projector screen instead.
**Root cause:** No anchor object was named in the prompt, so the model had no fixed reference point and guessed the entry point.
**Fix:** Name the door explicitly as the anchor every time: "she enters through the door, across from the projector and map" — never just "she enters the room."
**Trials wasted before fix found:** 6–7
