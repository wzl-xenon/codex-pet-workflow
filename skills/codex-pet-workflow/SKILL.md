---
name: codex-pet-workflow
description: Create, repair, extend, QA, and install Codex animated pets from one or more character images. Use when a user wants to turn a suitable image, mascot, avatar, generated character, or existing pet idea into a Codex pet; verify the initial character design before animation; build 8x9 or extended sprite atlases; define normal/tired/damaged/depleted states; package pet.json; debug renderer, sidecar, hot-switching, or Codex Desktop pet installation behavior. Includes Lingxi as a worked example.
---

# Codex Pet Workflow

## Overview

Use this skill as the planning and execution wrapper for making Codex pets from arbitrary character images. It complements `$hatch-pet` for atlas assembly and `$imagegen` for raster generation or redraws.

The central rule: lock the character first, animate second, install last.

## Decision Flow

1. **Input image or concept**: Read `references/character-intake.md`. Extract identity anchors and decide whether the source is strong enough for pet production.
2. **Character confirmation**: Produce or request a still preview, model sheet, or first-frame sample and ask the user to confirm the character before full animation unless the user has already approved it explicitly.
3. **Atlas production**: Read `references/production-stages.md`. Build the normal form first, then state variants, then optional higher frame-rate or extended-column atlases.
4. **Example alignment**: Read `references/lingxi-case.zh.md` when the user mentions Lingxi/灵汐 or when a concrete worked example would help preserve quality.
5. **Runtime integration**: Read `references/runtime-integration.md` before changing `pet.json`, sidecar logic, renderer hooks, hot switching, or Codex Desktop installation.

## Working Rules

- Prefer a reversible workspace copy before touching the installed Codex pet directory.
- Never delete existing pet assets, backups, generated frames, or renderer patches unless the user explicitly approves deletion.
- Use structured image/atlas tools from `$hatch-pet` where possible instead of hand-editing sprite positions.
- Treat PowerShell Chinese text display as unreliable; verify UTF-8 content with file reads instead of console appearance when Chinese names or notes matter.
- Keep pet identity consistent across frames: silhouette, face shape, hair, outfit landmarks, palette, accessory placement, scale, and ground contact.
- Do not claim hot switching works until it has been tested in the current Codex runtime or logs show the renderer reloaded the intended asset.

## Character Confirmation Gate

Before generating a full atlas from an image, confirm these anchors with the user:

- Character type, age impression, personality, and mood.
- Silhouette and proportions, especially head/body ratio for chibi pets.
- Hair shape, face, eyes, outfit layers, signature accessory, and color palette.
- What must be preserved exactly and what may be stylized for tiny animation cells.

If the user says the first preview is wrong, revise the character guide or redraw seed before producing new animation rows. Avoid "fixing" identity drift by darkening, recoloring, or stretching a wrong frame.

## Output Expectations

For a finished pet task, leave behind:

- A source or design brief describing the locked character.
- A QA contact sheet or preview of the atlas.
- The pet atlas image and `pet.json`.
- Notes about frame count, cell size, supported states, and any renderer/runtime assumptions.
- Installation status, test result, and remaining risk if the installed Codex app must be restarted.
