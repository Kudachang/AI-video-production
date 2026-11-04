---
name: "anamorphic-look"
description: "Use when an image or video prompt needs a real anamorphic film look: focal choice, oval bokeh, horizontal flares, anchored blur, film stock and the tech tail."
---

# Anamorphic look

Adapted from Higgsfield's anamorphic skill (Oct 2026). The model doesn't obey the lens name; it obeys visual evidence of the lens. Write that evidence in. Prompts stay in English. No brand, camera, lens or film manufacturer names in the prompt; describe the look, not the label.

## 1. Focal length by job

| Job | Focal | Diagonal FOV |
|---|---|---|
| Location, establishing, geography | 24mm | ~84° |
| Location with a hero object or depth layers | 35mm | ~63° |
| Tight interior, narrow street, vehicle | 40mm | ~57° |
| Medium shots, performance | 50mm | ~47° |
| Portrait, inserts | 85mm | ~29° |

Never shoot faces on 24mm. Character plates: 85mm portrait, 50mm full body, 35mm groups. For video generators, write the field of view in degrees: "84° diagonal field of view, anamorphic rectilinear character. Lens locked for the whole shot."

## 2. Anchor the blur in physics

"Strong blur" alone does nothing on a wide lens. Always write:
1. Focus point: one named object ("focus locked on the edge of the first column").
2. Distance: camera 1-3 m from the focus point, lens at knee, waist or chest height.
3. Aperture: wide open.
4. What dissolves: name the foreground and background layers that melt into soft blur.

## 3. Bokeh and flare as objects

```
anamorphic bokeh with elongated vertical oval highlights on [the wet floor / the lamp bulbs / the window glow] and a long horizontal blue streak flare off [the brightest light source in frame]
```
- Ovals are vertical; streaks are horizontal.
- Name the source of the flare. A warm source (tungsten, fire) gets a warm-orange streak, not blue.
- No bright source in frame, no streak: give the frame one highlight.

## 4. Film stock by light

| Scene | Wording |
|---|---|
| Night, interiors, dusk, tungsten | tungsten-balanced 500-speed colour negative film grain |
| Daylight, overcast, pastel | daylight-balanced 250-speed colour negative film, fine grain |

## 5. Tech tail (locations)

```
Shot on real 35mm film, [stock]; anamorphic [24/35/40]mm lens with subtle horizontal flare and gentle highlight bloom; rule-of-thirds composition; natural true-to-life color; realistic environment physics — [dust / haze / rain / drifting smoke]; gritty documentary film realism, indistinguishable from a real photograph, absolutely no CGI or render look. No cloned or duplicated elements. Clean environment plate, no characters. No text, no watermark, no logo. Aspect ratio 2.39:1.
```
Rain only reads when backlit and falling in visible streaks; say so.

## 6. Camera anchor

"Three-quarter angle, camera set to one side looking diagonally [across the room / into the depth], lens at [knee / waist / chest] height." One camera, one side, one height.

## 7. Aspect ratio

Default 2.39:1. Write it in words at the end and set it in the UI (21:9 where only presets exist).

## 8. Assembly order (location)

1. "Cinematic film still." + location in one line + mood
2. Camera anchor
3. What's in frame, foreground to background
4. Palette in a 60/30/10 split
5. Lighting: source, colour temperature, direction, contrast
6. Focus point, aperture, what dissolves, bokeh and flare objects
7. Tech tail

## 9. Failure fixes

| Symptom | Fix |
|---|---|
| Everything sharp | Name the focus point, camera 1-3 m from it, "wide open" |
| Round bokeh | "elongated vertical oval highlights" and name what they sit on |
| No flare | Add one bright source and name the streak off it |
| Fisheye distortion | Add "rectilinear", drop to 35mm |
| Stretched face | Switch from 24mm to 85mm or 50mm |
| Looks like a 3D render | Keep the full tech tail |
| Blue flare on a warm lamp | Change the streak to warm orange |
| A logo appears | A product was named somewhere; describe the look instead |

## 10. Negatives

Write removals positively ("uniform tone edge to edge" rather than "no gradient"). The tech tail's own "No cloned... No text..." lines are the only accepted exceptions.