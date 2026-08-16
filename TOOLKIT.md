# AI Video Production Toolkit

⚠️ **AIGC tools evolve fast.** Everything below is dated. If an entry is old, verify it still applies before relying on it — model versions and platform rules change often.

---

# The Simple Guide: How to Keep Characters, Props & Locations Consistent in AI Video
### Date: August 16, 2026

*A plain-language guide, based on what we learned studying Higgsfield's Cully Hill Boys production.*

---

## The One Big Idea

**Never ask the AI to draw something from scratch more than once.**

Instead:
1. Draw it ONE really good time. This is your "anchor."
2. Every time after that, don't describe it again — show it the anchor picture and say "keep this exactly the same, just change ONE small thing."

Think of it like a photocopier, not an artist. You're not asking for a new drawing every time. You're asking for the same drawing with one small edit.

---

## Why This Matters

When you describe a character or prop in words every single time, the AI redraws it slightly differently each time — that's why things "drift" (T-Hex looking a bit different shot to shot, a face looking slightly off).

When you show it a picture and say "keep it the same, change only X," it barely drifts at all.

---

## The 3-Step Template (works for characters, props, AND locations)

Every prompt has three parts, in this order:

### Step 1: LOCK IT
Say what must NOT change. Be specific — list the actual things.

> "Keep the same face, same pose, same outfit, same lighting, same background. Do not change anything else."

### Step 2: NAME THE ONE CHANGE
Say exactly what's allowed to change — just one thing, described clearly.

> "Only change the jacket color from black to red."

### Step 3: CLOSE IT
Repeat that everything else stays untouched. This is a safety net — it stops the AI from "helpfully" changing extra stuff.

> "Everything else — face, pose, background — remains exactly the same."

---

## Real Examples

### Example 1: Character (like Punky or Akari)

> Keep the same person, same face, same pose, same outfit, same lighting, same background.
> Only change: give him a scar across his left eyebrow, small and healed-looking.
> Everything else stays exactly the same — face shape, expression, clothes, background.

### Example 2: Prop (like T-Hex)

> Do not redraw, restyle, recolor, or move anything. Every part of the image should look exactly like the original photo.
> The only change: the left shoulder panel is dented inward, like it hit something hard.
> Nothing else changes — same paint, same lighting, same angle, same background.

### Example 3: Location (like the briefing room or refinery)

> This is the exact same room as the reference photo. Keep every object the same — the same crates, same lighting, same wall texture. Change nothing about the room itself.
> Only change: move the camera to show the room from the left side instead of straight-on.
> Everything else — objects, lighting, colors — stays identical.

---

## The "Cheat Sheet" Prompt Formula

Copy this and fill in the blanks:

```
Keep the same [face / object / room] — [list 2-4 things that must stay identical].
Only change: [describe ONE thing, specifically].
Everything else stays exactly the same.
```

For props specifically, add this stronger warning at the start — it works better for objects than for faces:

```
Do not redraw, restyle, recolor, or re-light anything. 
Keep every part pixel-identical to the original.
[then continue with the formula above]
```

---

## One More Tip: Build a "Reference Sheet" First

Before you generate ANY shots of a character, prop, or location — spend one generation making a really good multi-angle reference:

- **Character:** front view + back/side view + close-up face, all in one image
- **Prop:** 2 full views from different angles + 2 close-ups on the details that make it recognizable (a logo, a dent, a texture)
- **Location:** one clear wide shot showing the whole space

This becomes your "anchor" — the ONE picture you'll keep showing the AI and editing from, instead of redrawing from words every time.

---

## Quick Recap

| Old way (causes drift) | New way (stays consistent) |
|---|---|
| Describe the whole thing in words every time | Show a picture, describe only the change |
| "A robot with a dented shoulder, blue eyes, standing in a warehouse..." | [photo of T-Hex] + "only dent the left shoulder, nothing else changes" |
| Hope it looks the same | Lock it, name the one change, close it |

**Bottom line: Build it once. Edit it forever. Never redraw from scratch.**

### Note: negative-phrasing prop-lock — tool-specific

The "Do not redraw, restyle, recolor, or re-light anything" prop-lock
phrasing (see Simple Guide, Aug 16 2026) is confirmed working in
**Nano Banana Pro** and **GPT Image 2** (source: Cully Hill Boys prompt
screenshots).

It has NOT been confirmed in **Cinema Studio** — and per the existing
rule above, Cinema Studio 3.0 has no negative-prompt support, so
"do not X" phrasing may not work there.

If using the prop-lock trick inside Cinema Studio, rephrase as a
positive instruction instead:

❌ "Do not redraw, restyle, recolor, or re-light anything."
✅ "Keep every part of the image pixel-identical to the original —
    same paint, same lighting, same angle, same background."

Rule of thumb: outside Cinema Studio, negative phrasing is fine to
try. Inside Cinema Studio, always convert "don't do X" into "do Y"
instead.

### Prepared by Claude with supervision from Bill, August 16, 2026

---

## Technique: Lock Geometry First, Animate Second
*Added 2026-08-12. Verify this is still relevant before relying on it — model capabilities for spatial accuracy move fast, and this technique may become unnecessary as models improve.*

**Use when:** a shot keeps failing on spatial/positional accuracy (wrong seat, wrong side of room, wrong facing direction, wrong entrance point) after multiple prompt rewrites — wording alone isn't fixing it, and the same wrong default keeps appearing.

**Why this happens (as of 2026-08-12):** video/image models carry strong statistical bias toward the most common version of a given composition in their training data (e.g. "back row" in a theater/briefing-room shot, "enters from the visually obvious side" in an establishing shot). Past a certain point, more precise wording stops helping — the model isn't failing to understand the instruction, it's actively defaulting against it.

**How to tell you've hit this wall, not a wording problem:**
- The same spatial error persists across multiple structurally different prompt attempts (prose, negative constraints, anchor objects, labeled sections, timestamps, plain-language rewrites)
- A schematic/diagram reference doesn't fix it either
- It fails the same way in both video and static-image generation

**The fix — split into two separate problems, don't solve both at once:**

1. **Lock the geometry as a static image first.** Get one correct still where every element (character position, facing direction, object placement) is right — by any means necessary: multiple regeneration attempts, a different tool/model, manual compositing, or an external AI (e.g. having another model attempt the same still and cross-checking). Don't move on until this single frame is fully correct.
2. **Animate motion on top of the correct still, not from scratch.** Use the locked-correct image as the sole/primary reference for the video generation. Only ask the model to add camera motion or minor animation — not to also solve placement at the same time.
3. **Favor the model's natural motion bias.** Push-in is generally an easier, more default-aligned move for these models than pull-back/reveal, as of 2026-08-12. If the shot calls for a pull-back, generate a push-in instead and reverse the clip in post (Jianying: select clip → 倒放/Reverse). Same applies to other move pairs where one direction is closer to training-data default than its opposite. **Re-test this assumption periodically — model defaults shift with new versions.**
4. **Mute/replace baked-in audio after reversing** — reversed audio (footsteps, hums with directional character) can sound wrong even when the reversed video looks fine.

**Bottom line:** if a shot needs correct spatial placement *and* correct camera motion, and it's failing, stop trying to get both from one generation. Nail the geometry as a still, then only ask for motion.

**Status check log:**
- 2026-08-12: Confirmed working, this session, on Seedance/Lovart for a briefing-room seat-position failure.

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
