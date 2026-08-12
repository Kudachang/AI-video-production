# Issue Log

Real production mistakes and fixes. **Newest first.** Don't delete old entries — mark them outdated if a fix stops working, but keep the history.

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
