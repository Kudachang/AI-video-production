# Issue Log

Real production mistakes and fixes. **Newest first.** Don't delete old entries — mark them outdated if a fix stops working, but keep the history. Chronological order, latest first.

---

## 2026-08-12 — Seat-position failure, briefing room reveal shot (RESOLVED)

**Problem:** Camera positioned behind Punky, over-the-shoulder toward a projection screen, with a pull-back/reveal move. Punky repeatedly generated in the second row of chairs instead of the correct first row (closest to the screen), regardless of prompt wording.

**Attempts made (15-20+ rounds, all failed to fix the seat alone):**
- Plain prose position description
- Explicit negative constraints ("NOT in the second row")
- Anchor-object framing, first relative to the projector, then relative to the projection screen
- Structured/labeled prompt format (ROW DEFINITIONS, POSITION, NEGATIVE, CAMERA as separate blocks)
- Timestamped action beats ([0-2s], [2-8s])
- Full "assume zero memory" plain-language rewrite from scratch
- Custom top-down floor-plan diagram (schematic, labeled, chairs/projector/door/screen/Punky's seat marked) uploaded as an additional reference image
- Attempted as a static image instead of video, to simplify — also failed twice

**Root cause (diagnosed via Gemini):** Strong training-data bias in video/image models toward "middle or back row" seating in over-the-shoulder theater/briefing-room compositions — this is the statistically dominant pattern in training data for this shot type, and it actively resists correction through prompt wording alone, no matter how explicit.

**Fix that worked:** Stopped trying to solve spatial placement and camera motion in the same generation. Instead:
1. Generated a corrected static still with the seat position right (external tool succeeded where Seedance/Lovart repeatedly failed on this specific spatial task).
2. Used that correct still as the sole reference for a **push-in** video generation (not pull-back) — push-in is the model's natural/default camera-motion bias, so this avoids fighting the model on two fronts at once.
3. Reversed the resulting clip in Jianying (剪映) to get the pull-back reveal effect actually needed for the scene.

**Lesson for future shots:** When a generation keeps failing on spatial/positional accuracy, stop iterating the prompt and separate the problem into two stages — (1) get a single correct still image locked first, by whatever means necessary, then (2) only ask the video model to animate motion on top of that already-correct geometry, ideally motion in the model's natural bias direction (push-in over pull-back), reversing in post if the opposite motion is what's actually needed.

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
