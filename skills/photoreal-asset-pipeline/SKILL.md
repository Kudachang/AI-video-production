---
name: "photoreal-asset-pipeline"
description: "Use when building photoreal AI image assets for film previz: character sheets, wardrobe, prop specs, set sheets, environment variants and start/end frame pairs for video."
---

# Photoreal asset pipeline

Goal: consistent, reusable image assets that read as live-action film stills, not CGI. Video prompt craft lives in seedance-director; this skill covers the images that feed it.

## Build order
1. Face and body truth: multi-angle headshots (front, 45 L/R, chin-down, low angle) and full-body front/back/profile. Generate once, then treat as immutable.
2. Wardrobe: headshot as identity anchor plus a garment image as second reference.
3. Headless mannequin and 360 turnaround for wardrobe and props, so the face doesn't interfere.
4. Prop sheets: isolated on white, multi-panel, scale checked against the body.
5. Set sheets: max 4 panels, then extract the winning panel and upscale to 2K.
6. Environment state variants (intact, collapsed, burning): always derived from the named master view.
7. Shot design: start/end frame pairs with a composition lock.

## Rules
- Degradation reset: never edit an edit past about 3 generations. When skin turns waxy or plastic, restart from the original character sheet and location reference, not the latest composite.
- Narrowest edit wins: swap only the wrong element (e.g. only the gauntlets) instead of re-rendering the whole frame.
- Props: describe construction part by part, in order (frame, panels, plates, gem, pistons, straps, collar). Never "same as before".
- Count anatomy explicitly: "FOUR finger plates, FOUR knuckle guards". State orientation ("fist pointing up").
- Scale by body proportion, not adjectives: "the fist is as big as her head; cuff as thick as her neck". Use percentage changes (+40%) when a base image is supplied.
- Composition lock on every frame-pair call: "Identical crop, identical camera angle, identical lens, head stays at the same size and position. No zoom, no reframe, no camera move."
- Environment consistency: name one master view; derive every other angle from it explicitly. Independent "views" produce different sets.
- Reference roles: assign each image exactly one contribution (face / wardrobe / prop / location / pose). Separate "background only" from identity.
- What must not change: write it as a checklist, separating structure from surface ("the gauntlet holds; its plating breaks; the gem is mid-fracture").
- Invisible forces through the body: no energy rings or auras. Show skin ripple on cheek and jaw, flesh compression, airborne sweat, hair and debris direction.
- Material language beats style language: describe the physical material (weave, finish, grime, torn edges, "not chrome, not a graphic overlay"), not the vibe.
- Lighting = direction, not intensity: one named source ("8-9am sun from one side only", "the projector beam is the only light"). Avoid beauty-key lighting.

## Anti-CGI skin paragraph (append every time a face is in frame)
Pores across nose, cheeks and forehead; vellus hair catching side light; sweat beads; dust in creases; scars; uneven tone; oily T-zone; subsurface scattering on ears and nostrils; slight asymmetry; one continuous frame of film, exposed once, not composited, not retouched. 35mm anamorphic.

## Failure table
| Symptom | Fix |
|---|---|
| Plastic or CGI face | Restart from sheet; skin paragraph; single-source light |
| Wrong scale | Anchor to a body part or neighbouring object |
| Wrong count or orientation | Explicit counts and orientation; re-attach design image |
| Panels disagree | One master view |
| Start/end frames don't cut together | Composition-lock clause |
| Unusable grid panel | Extract the panel, upscale to 2K |
| Visible energy ring | Ban the effect; describe physical transmission |