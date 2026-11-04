---
name: "seedance-director"
description: "Use when writing, fixing or auditing AI video prompts for Seedance 2.0/2.5, MiniMax H3, Kling or Wan, especially action shots, fights, reference kits and multi-beat clips."
---

# Seedance Director

Condensed from Serge Shima's visual-skills (video skill), CC BY 4.0. Attribution: Serge Shima, github.com/smixs/visual-skills. Full version with all reference files: clone that repo. Section 13 adapts techniques from Higgsfield's "How to Make a Cinematic AI Short Film" workflow (Oct 2026) and its fight-scene skill.

Direct first, then write the prompt. A beautiful frame with no dramaturgy is wallpaper. A prompt with no physical detail is mush.

## 1. Before writing: the shot must do a job

Every shot must do at least one of: change emotion, advance action, or increase pressure. If it does none, cut it.

Every shot owns three physical details (the Details Law):
- one environmental pressure (dust in a light shaft, wet asphalt, cold light)
- one micro-action of the body (jaw locks, knuckles whiten, breath catches)
- one sound anchor or visual motif

Named emotions without a body do not render. Write the jaw, the breath, the eyes, not the word "angry". For performance, give the eyes a task (see the acting-task skill).

Banned words: cinematic, epic, stunning, masterpiece, beautiful lighting, hyperrealistic 8k. Each one is a placeholder for a detail you failed to invent. Replace with lens, light source, texture and grain.

Rhythm: long, shorter, shorter, pause, impact. The pause before the hit matters more than the speed of the cuts. For impacts, use a speed ramp: slow wind-up, snap to real speed on contact, slow aftermath.

## 2. Seedance 2.5 prompt formula

Base:
<Subject> performs <one primary action> in <scene>. Visual style. Shot size, angle and camera move. Audio.

For reference-heavy or longer clips:
reference declaration + one-line summary + plot by timeline + global tail (restate must-hold rules).

Duration, ratio and resolution go in the generation settings, not the prompt.

## 3. Reference discipline (most common failure)

Write the role of every attached image in the prompt. Bind each subject separately:
- "@Image 1 defines Punky's face, hair and clothing. Use only her appearance. Do not use the image background."
- "@Image 2 defines the gauntlet design only."
- "@Image 3 defines the location and lighting only. Do not copy its camera angle."

Never write "Images 1 to 4 are the four characters". State which is which.

The model copies whatever is in a reference: its camera angle, its scale, its orientation, its props. If you want a new angle, either drop the background image or exclude its angle in words. If a prop must not appear (a weapon, a second fist), remove it from the reference image, because text rarely overrides a reference.

When orientation keeps coming out wrong (a prop facing the wrong way), stop rewriting the text: generate a still with the correct orientation and use it as the start frame. For hard physics beats, give both a start frame and an end frame.

Drop any reference that duplicates another; redundant references dilute the binding.

One subject per image beats a collage. The same character in two states (intact vs damaged) needs two images, each bound to its time range, and is the flakiest binding.

Repeat the @ mention of a key reference later in the prompt to strengthen it.

## 4. Timing

- Split a clip into stages. One primary state change per stage, and always state the visible end state.
- Time windows of 3 seconds or more. One core action and one camera move per window.
- Ranges are consecutive, never overlapping. A range is a time budget, not a cut point.
- Too much in one window causes omissions or merged actions. When a multi-action clip fails twice, split it into separate clips and join them on action in the edit.

## 5. Realistic humans

Character = age/ethnicity + skin texture + 3-4 facial details + gaze + hair + clothing fabric + build/aura.

Always append: "retaining real fine pores and skin texture". Add sweat, dust in skin creases, film grain, a single practical light source. For one emotional shift, give 2-4 observable cues (eyes, brow, mouth, breath, throat). More reads as overacting.

For weapon or prop inserts that keep getting blocked, use a headless mannequin wearing the prop, close-up.

## 6. Physics

- Declare the physics regime up front: "metal, dust and debris obey real-world physics."
- Narrate consequences, not just actions: the hit dents the plate, the shockwave blows dust outward in a ring, stones bounce.
- State the wanted state positively first: "the machine keeps metallic rigidity"; "her right hand rests at her hip"; "every kick stays below belt height". Use a negative only for a known collapse that a positive can't express, and never name a thing you don't want to see (see 13).
- Gate events on triggers: "at the moment the gauntlet touches the lens, the camera jolts."

## 7. Camera

Understood terms: extreme wide, wide, medium, close-up, extreme close-up; push in, pull out, pan, tilt, orbit, follow, handheld, low angle, overhead, POV, one-take, dolly zoom, bullet time, speed ramp. For rare terms, add the visible result: term + subject + what changes in frame + direction or speed.

Locked frame: write "Locked-off camera on a tripod, no pan, no zoom, no orbit." "Static" alone drifts.

State scale with anchors and ratios: "its head is level with the temple roof", "she reaches its knee", "the double fist covers half the skull's width". "Huge" alone fails. Scale corrections work in percentages ("20% smaller").

Wide lenses near the camera inflate foreground objects. Use a telephoto (85mm) and "at the same distance as the subject" to keep scale honest. For lens character, see the anamorphic-look skill.

One-take that keeps cutting: "one continuous shot, no cuts of any kind", plus a camera path that never motivates a cut; if it still cuts, shorten to 10-15s.

## 8. Audio markers (Seedance 2.5)

- Music ( ), sound effects < >, dialogue { }, on-screen text 【 】.
- Ban line that works in 2.5: "Pure video, no subtitles, no background music." Repeat it in the global tail.

## 9. Blockout / white models

- A gray-model previz video can lock camera path, staging and scale. Map every primitive to a reference: "the tall shape in @Video 1 is RoboRex". Exclude its look: "do not use its gray geometry or empty background."
- Coarse blockouts with simple primitives work better than detailed ones. Avoid limbed mannequins unless you also write the full limb motion; they go stiff.
- A top-down camera-path sketch can be an image reference: "follow the camera route in @Image N".

## 10. Editing and extension (Seedance 2.5)

- Edit an existing clip: name it the sole editing master, list everything to preserve, then the one change. Keep sources at 20s or less. One edit target per pass.
- Extend: "the first frame of the extension continues directly from the last frame of @Video 1; keep pose, props, camera position, lighting, motion direction." Ceiling 60s.

## 11. Model choice

- Seedance 2.5 errs by commission: it executes nearly every instruction but may misuse a reference. Best for precise timing and dense choreography. Strictest filter on realistic faces with violence.
- MiniMax H3 errs by omission: more filmic overall but drops listed beats. Needs more explicit detail per beat.
- Kling 3.0: best for multi-character dialogue up to 15s, and for start-frame/end-frame physics shots. On Higgsfield it takes only start and end images, no reference images.
- Wan 3.0: accepts image references, up to 1080p, fairly realistic; a good fallback when Seedance blocks.
- On Higgsfield, Seedance 2.5 (omni_reference) needs at least one reference and tops out at 1080p; a job status of "nsfw" means blocked, no video.

## 12. Pre-flight check (run before every prompt ships)

1. One primary action per clip, or per 3s+ window (or one hit per shot in a fight block).
2. Every reference has a stated role and exclusions.
3. Three details per shot: environment, body micro-action, sound or motif.
4. Scale stated with an anchor or ratio.
5. End state of the shot stated.
6. Known collapse points written as positive states, not as named negatives.
7. No banned filler words, no martial-arts jargon.
8. Audio line present.

If a prompt fails twice, change the structure (split, new reference, new angle, start/end frames, re-coverage) instead of adding more words.

## 13. Fights, coverage and the "named = summoned" rule

- **Named = summoned.** Naming what must not appear tends to make it appear ("no high kicks" produces high kicks, "no green" can add green). Write the wanted state instead: "every kick stays below belt height", "the first visible motion of a limb IS the strike itself". If a prop must not appear, remove it from the reference image.
- **No martial-arts or technical jargon in the prompt body.** The model doesn't know the term and renders generic action. Describe body geometry: "almost side-on, right shoulder and right foot leading, rear heel floating".
- **Uncommon strikes need three anchors:** an everyday analogy ("like a tennis backhand", "like stamping a door"), the striking surface (what touches first, which way the palm faces), and the reaction along the strike vector (a backhand snaps the head sideways).
- **Beats of 1-2 seconds:** position, then action (which limb, trajectory, target), then the opponent's physical reaction, then the new position.
- **Broken rhythm:** explosion, complete stillness, explosion. Write stillness as a state.
- **Fight block format:** a 30s clip of one-hit shots joined by hard cuts at exact timestamps (2.0, 4.0, 6.0 s...). Each hit approaches in slow motion and snaps to real speed on contact; cut on the end of the reaction. Keep the whole fight within one named zone of the location so the room stays consistent.
- **Blocking diagram:** a top-down sketch marking each fighter's start position. Declare it as positions only, not a camera reference.
- **Re-coverage:** feed a finished clip as the source; "every movement happens at the same second, in the same place, with the same result; only the camera and speed change." Use it for new angles, or to re-render a clip with corrected props by adding the prop reference.
- **Character video elements:** a short clip of the approved character (three-quarter view, small head turn, a blink, a breath, their voice) anchors identity better than a still across many shots.
- **One prompt, several takes:** keep the best passage of each and join them, hiding joins in whip-pan blur or body movement.
- **Relight-only edit:** "Keep this exact frame. Same camera, lens, composition and objects. Change only the lighting."
- **Prompt density:** dense 30s multi-shot prompts work on Seedance 2.5 via Higgsfield. Test one before abandoning the short-prompt rule; on Seedance 2.0 keep prompts short.
- **Violence that passes:** describe what the camera sees, not the injury ("skin unbroken, the break is inside, read as the turned head and the body falling").

---
Attribution: Serge Shima, github.com/smixs/visual-skills (CC BY 4.0). Condensed and adapted.