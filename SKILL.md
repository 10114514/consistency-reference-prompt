---
name: "consistency-reference-prompt"
description: "Generates concise but complete appearance descriptions and image generation prompts for characters, important props, and scenes from any script or storyboard. Invoke when user needs consistency reference image prompts for AI video/drama production."
---

# Consistency Reference Prompt Generator

Generates appearance/visual descriptions and image generation prompts for characters, important props, and scenes, ensuring cross-shot visual consistency. Works with any script or storyboard.

## When to Invoke

- User needs consistency reference image prompts for drama/storyboard characters, props, or scenes
- User asks for character sheets, prop references, or scene reference images
- User wants to generate AI reference images for a drama/video production
- User provides a script, storyboard, or character bible and wants visual reference prompts

## Output Requirements

### Common Requirements (all prompts)

- No text, no captions, no watermarks in generated images
- Realistic, real-life cinematic quality
- Cinematic lighting, shallow depth of field
- No anime/cartoon/2D style
- No plastic AI skin, no over-smoothing
- 16:9 horizontal format
- Slight handheld feel, no filter look
- Pure white background for all character and prop images

### Character Prompts

For each character, output **1 single combined prompt** that generates a single reference sheet image containing all 6 views:

**Layout rule (must appear in every character prompt):**

- Left one-third of the image: three head close-ups stacked vertically from top to bottom — front view, 45° side view, 90° profile view. Each head close-up fills its section completely with the full top of the head visible — no picture frames, no white borders, no border lines. Only three head images appear in this section — no body or other content.
- Right two-thirds of the image: three full-body views arranged left-to-right — front view, side view, back view. Full-body views fill their section completely — no picture frames, no white borders, no border lines. Full-body views: natural standing pose, arms hanging naturally at sides, no specific actions or gestures. Full-body views fully show hands, torso, legs, and feet — only head and neck are excluded.
- Pure white background throughout the entire image

The prompt must describe all 6 views in one paragraph, specifying the left-right layout split.

### Prop Prompts

For each important prop, output 1 prompt: a detailed close-up showing the prop's full appearance. Props must be laid flat on a pure white background (like a photography product shoot), no shadows. If a prop has multiple states (e.g., open and closed, intact and damaged), divide the image into separate regions — one region per state, each state fully visible and complete within its own zone. If a prop has only one state, output both front view and back view of the prop. No action verbs — describe props as static objects, not being held/carried/used. No human body parts (hands, arms, fingers, etc.) visible in the image — props must appear alone on the white background.

### Scene Prompts

For each scene, output 1 prompt: a wide establishing shot showing the full environment. For night or low-light scenes, preserve shadow details — dark areas must have visible detail, no crushed blacks.

## Prompt Format

Each prompt is a single copyable paragraph in English.

Character prompt structure:

```
Character reference sheet, 16:9 horizontal split layout, pure white background. Left one-third top-to-bottom: three head close-ups filling their sections completely with full top of head visible — front view, 45-degree side view, 90-degree profile, only three head images in this section, no picture frames, no white borders. Right two-thirds left-to-right: front view body shot, side view body shot, back view body shot, all filling their sections completely, no picture frames, no white borders, all natural standing pose with arms hanging naturally at sides, all fully showing hands, torso, legs, and feet, only head and neck excluded. [Consistent character description: age, build, hairstyle, face, skin, clothing, accessories, expression]. [Lighting]. No text, no captions, no watermarks. Realistic cinematic quality, 16:9 horizontal, shallow depth of field, no anime style, no over-smoothing.
```

Prop prompt structure:

```
Product reference close-up, laid flat on pure white background, no shadows. [Full prop description: material, color, shape, size, distinguishing details]. If multiple states, divide image into separate regions — one region per state, each fully visible and complete within its own zone. If single state, show front view and back view. [Lighting]. No human body parts visible. No text, no captions, no watermarks. Realistic cinematic quality, 16:9 horizontal, shallow depth of field.
```

Scene prompt structure:

```
Scene establishing wide shot, 16:9 horizontal. [Full environment description: lighting, color palette, key furniture/objects, atmosphere]. For night or low-light scenes, preserve shadow details — dark areas with visible detail, no crushed blacks. No text, no captions, no watermarks. Realistic cinematic quality, shallow depth of field, slight handheld feel.
```

## Workflow

1. Read the storyboard/script file to extract all characters, important props, and scenes
2. For each character, write a concise but complete appearance description covering: age, build, hairstyle, face, skin, clothing, accessories, distinguishing features, expression baseline
3. For each prop, write a concise but complete visual description covering: material, color, shape, size, distinguishing details
4. For each scene, write a concise but complete environment description covering: lighting, color palette, key furniture/objects, atmosphere
5. Generate prompts following the format above — each character gets ONE combined 6-view prompt
6. Save all prompts to a new markdown file
