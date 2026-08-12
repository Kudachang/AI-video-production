# AI Video Production Toolkit

⚠️ **AIGC tools evolve fast.** Everything below is dated. If an entry is old, verify it still applies before relying on it — model versions and platform rules change often.

---

## 2026-08-12 — Initial toolkit (source: Higgsfield Cannes Manual + OSideMedia/higgsfield-ai-prompt-skill)

### Tool selection notes (your own findings)

| Tool | Best for | Weak point |
|---|---|---|
| **Seedance** | Mechanical/prop-heavy characters (gauntlets, armor), highest overall quality | Stricter — harder to nail exact wardrobe/props |
| **Higgsfield** | Clean human-only scenes, built-in AI director works well | Struggles with precise mechanical/prop rendering |
| **Lovart** | Content that Higgsfield blocks (censorship-sensitive shots) | — |

Rule of thumb: mechanical/prop-heavy → Seedance. Human/dialogue-driven → Higgsfield. Blocked on Higgsfield → try Lovart before giving up on the shot.

### Seedance 2.0 — hard engine rules

These are stated as hard constraints of the engine, not tips.

- **Describe intent + named technique, not biomechanics.** ✅ "spinning back kick connects" ❌ "left forearm rotates 45° to deflect..."
- **Describe force + result, not the impact itself.** ✅ "driven into the car, metal buckling" ❌ "slams into the door, glass shatters" — naming the impact directly causes the model to fill gaps unpredictably (confirmed: this caused a "flies in like Superman" failure in testing).
- **Re-anchor position and facing direction after every cut.** The model doesn't remember where someone was standing.
- **Track 3 characters max across cuts.**
- **Exit-frame = implicit cut.** A character who leaves frame is gone for the rest of that shot. Never choreograph exit + re-entry in one continuous shot.
- **A location needs a named entry/anchor point, or the model guesses.** Confirmed: a character entered through the wrong side of a room (a projector screen instead of the door) because no anchor was named.
- **Off-screen = nonexistent.** Only describe what can be seen or heard.
- **Avoid reflection shots** (blades, puddles, mirrors) — breaks scene geography.
- **Micro-expressions as physics, not adjectives.** ✅ "jaw clenches, nostrils flare" ❌ "looks angry"
- **Every cut changes both shot size and camera character** — never repeat the same camera mode across a cut.

### The 28 Hacks (condensed)

**Prompting**
1. Emotion = anatomy, not adjectives
2. Real camera language ("anamorphic prime, f2.8, film grain, halation"), not "cinematic"
3. Build a system prompt first — lock character/location/style before generating
4. Every generation is diagnostic — batch of 4, fix what's wrong, regenerate
5. Timestamped beats for shots over 4–5s: [0–2s] [2–5s] [5–8s]
6. One prompt can hold multiple cuts: Establish → Action → Reaction
7. Phonetic spelling for invented names: "Gan-del-FEE-nah"
8. Write edit decisions into the prompt (cut timing, angle, who to cut to)
9. Screenshot best frame → Claude describes it cinematically → reuse
10. Tell Claude "update only what changed" — saves ~80% tokens on iteration
11. Compress prompts over ~400 characters instead of layering more fixes

**Pre-Production**
12. 60:30:10 color rule per scene
13. Wide shot first for dialogue scenes, then medium, then close-up
14. **One anchor object per location — name it every time.**
15. Never shoot a location dead-on from the front
16. 4 reference views per location: exterior, interior wide, interior 3/4, detail
17. Top-down spatial map for any 2+ character scene, built before prompting
18. Action sequences get a script: Setup → Action → Consequence
19. Crop the face out of character sheets before uploading
20. Body-integrated props need 3 views: exterior, attachment point, detail seam
21. Restate injuries/clothing/props every generation — nothing carries over

**Teamwork (solo-adapted)**
22. Deliberate cold-review pass — don't approve in the same session you generated
23. One dedicated final "slop check": fingers, eyelines, warped text, physics, identity drift
24. One shared source of truth — this repo

**Editing**
25. Review frame by frame before locking
26. FPS drops = usually duplicated frames — delete them, don't regenerate
27. Salvage failed generations — 2 good seconds inside a bad clip is still usable
28. You can always regenerate — don't accept "close enough"

### Negative Constraints / Artifact Reference

**Body / Motion**
| Artifact | Fix |
|---|---|
| Floating/extra limbs | "Anatomically correct, all limbs visible and naturally positioned" |
| Limb merging | Keep characters at arm's length; "distinct body separation" |
| Jittery motion | 1 primary action + 1–2 secondary max per clip |
| Motion morphing on fast action | Generate in Slow Mo, speed up in post |
| Named martial arts moves failing | Use the move's name/intent only, not joint mechanics |
| Grappling renders as embracing | Plain text not @Elements; describe positions not grapple names |

**Face / Identity**
| Artifact | Fix |
|---|---|
| Face morphing/shifting | Soul ID for multi-shot work |
| Identity drift across shots | **Separate Identity Block (face/wardrobe/body) from Motion Block (action) — never mix them in one prompt** |
| Character swap (2 characters) | @Elements only in static scenes; plain text for action |
| Wrong/frozen expression | Micro-expression terms as physics; one emotion per shot |
| Plastic/waxy skin | Kling 3.0 or Soul Cast; add "natural skin texture, subtle imperfections" |

**Texture / Lighting**
| Artifact | Fix |
|---|---|
| Flickering textures | Commit to one named style, don't mix |
| Over-lit/flat lighting | Always specify source: "single side-light", "golden hour", "practical only" |
| Color grade inconsistency | Lock grade in a moodboard, repeat exact language every prompt |

**Temporal / Consistency**
| Artifact | Fix |
|---|---|
| Static I2V output | Only describe what CHANGES/MOVES |
| Camera movement not working | Exact preset name on its own line: "Camera: Dolly In" |
| Scene continuity breaking | Copy-paste description verbatim; lock moodboard |
| Lip-sync desync | Trim dialogue to 3–8s; remove head/face motion tokens |
| Background music overriding dialogue | Timestamp-anchor: "Audio @Audio1 plays exactly as uploaded from 0s to end"; remove ALL ambient/SFX/music tokens |

**Content Filter / Safety**
| Artifact | Fix |
|---|---|
| Blocked (horror/dark content) | Describe atmosphere not explicit acts: "unsettling", "dread" |
| Named real person blocked | Character description instead of real name |
| Brand/IP name blocked | Describe by appearance, never by name |
| Weapon/violence filtered | Describe tension/aftermath/impact, not graphic injury |

**Cinema Studio (if used)**
- 3.0 has no negative-prompt support — every constraint must be phrased positively. "No shaky camera" → "locked-off static camera, no movement."

### Standing rules going forward

1. Identity Block always separate from Motion Block, pasted verbatim every time.
2. Every location needs a named anchor before you shoot it.
3. Impacts described as force + aftermath, never as the impact action itself.
4. Body-integrated props get 3 reference views, uploaded separately from face references.
5. One primary action per clip.
6. Filter-sensitive content → atmosphere/aftermath language, or route to Lovart.

### Still to pull from source (not yet reviewed in full)

- `skills/higgsfield-soul/SKILL.md` — full Soul ID rules
- `FAILURE-MODES.md` — 11 named Seedance render failures
- Higgsfield FACS Director — facial expression coding system
- Higgsfield Audio Prompting Guide — 4-layer audio system
- The Hell Grind feature-film pipeline itself

Source repo: `github.com/OSideMedia/higgsfield-ai-prompt-skill`
