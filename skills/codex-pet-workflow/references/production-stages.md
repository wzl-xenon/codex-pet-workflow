# Production Stages

Use this reference after the character design is confirmed.

## Stage 0: Workspace Audit

Locate the current pet workspace, existing atlases, source frames, contact sheets, install scripts, renderer patches, logs, and backups. Work on copies inside the workspace first. Do not overwrite the installed pet until QA passes.

## Stage 1: Normal Form

Build the standard pet before adding variants:

- Confirm cell size and atlas grid.
- Keep scale, baseline, transparency, and cropping stable in every cell.
- Produce enough unique frames for each row; avoid duplicated cells disguised as animation.
- Generate a QA contact sheet and inspect edges for leaked neighboring-frame pixels.

Common native Codex layout:

- 8 columns by 9 rows.
- Rows usually map to idle, run-right, run-left, wave, jump, fail, wait, run, and review-style actions.
- The native renderer may assume 8 columns, so extended frame counts require renderer support.

## Stage 2: State Variants

Define states as separate visual forms with shared identity:

- **normal**: clean default character.
- **tired/small-broken**: lower energy, mild wear, softer posture; do not merely darken.
- **large-broken**: clear fatigue, stronger clothing damage or disarray, reduced confidence.
- **depleted/final**: collapsed, exhausted, or unable to continue; motion should match the state.

When states are driven by token quota or usage, define thresholds in code and keep art names stable. Example thresholds: `<60%`, `<30%`, `<10%`.

## Stage 3: Animation Completeness

For higher frame rate, choose between:

- More unique frames at the same duration for smoother motion.
- Same frame count with longer/shorter timing for slower or faster motion.
- Extended columns, only if the renderer supports columns beyond 8.

Do not stretch cells narrower just to fit more frames unless the renderer and atlas metadata are changed together. Otherwise the pet will sample the wrong frame regions.

## Stage 4: Packaging

Package with:

- Atlas image with transparent unused cells.
- `pet.json` with name, atlas path, cell dimensions, rows/actions, and any state metadata supported by the runtime.
- Contact sheet and preview GIF/webm when useful.
- Notes about whether it targets native Codex pet loading, a sidecar renderer, or a patched renderer hook.

## Stage 5: QA

Check:

- No non-transparent slivers from neighboring cells.
- Left/right motion direction is correct.
- Character scale and feet/baseline do not jump unexpectedly.
- Damage states are actual redraws or intentional edited forms, not accidental filters.
- Installed runtime uses the expected asset and not a stale cached copy.
