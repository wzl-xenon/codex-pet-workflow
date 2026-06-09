# Runtime Integration

Use this reference before changing live Codex Desktop pet behavior.

## Native Pet Path

Native Codex pet loading is the safest path for ordinary 8x9 atlases. Prefer it when:

- The pet fits the native grid.
- State switching can wait for app reload or the current runtime already supports re-reading the pet asset.
- The user wants the least invasive install path.

Validate the active `pet.json`, atlas dimensions, and whether Codex Desktop must restart before the new asset is visible.

## Sidecar Path

Use a sidecar when:

- The native renderer cannot hot-switch state.
- The user wants dynamic behavior based on runtime signals such as token budget, task completion, or custom events.
- Experiments should not patch the installed Codex app.

The sidecar should read an explicit state file or local signal and render the pet independently. Keep the signal schema small and inspectable.

## Renderer Hook Path

Use a renderer hook only when native and sidecar paths cannot deliver the target behavior. Before patching:

- Back up the target app bundle.
- Re-discover renderer anchors after every Codex app update.
- Change one behavior at a time and keep install logs.
- Expect Microsoft Store or app updates to replace patched files.

For extended columns, the renderer must calculate background size and frame offsets from the actual column count. Preserve compatibility with existing 8-column pets.

## Hot Switching

A hot switch is real only when the currently running renderer observes a state or asset change and updates without restarting Codex. Check with:

- A manual state toggle.
- A visible frame or asset change.
- Logs proving the renderer received or polled the new state.

If a change appears only after restart, describe it as restart-applied, not hot-switched.

## Performance Debugging

If Codex stutters after task completion, inspect logs around the exact local time first. Look for:

- Repeated GIF/spritesheet regeneration.
- Asset reload loops.
- Renderer hook exceptions or retry storms.
- File watcher churn.
- Synchronous image decoding on the UI path.

CPU, GPU, and memory averages can look normal during short UI stalls, so logs and timing are more useful than overall utilization.
