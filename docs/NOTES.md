# FFXI Addon — Repeater

> [!NOTE]
> **Quick Reference**
> - **Path:** `C:\Windower\addons\Repeater\`
> - **Author / Version:** Selindrile (thanks to Balloon, Lorand, Mujihina) / v1.1
> - **Commands:** `//repeat`, `//repeater`
> - **Load Status:** `scripts/init.txt`
> - **Origin:** Third-Party (`https://github.com/Selindrile/Repeater.git`)

Repeatedly executes any configured Windower or in-game command on a configurable second-based interval for a set count or indefinitely.

## What the Code Does
- Stores three runtime globals: `autorepeat` (default `false`), `repeatdelay` (default `10` seconds), `line` (default `'input /echo Command to repeat has not been set.'`), and `count` (default `'Forever'`).
- Starting the repeater sets `autorepeat = true` and invokes `repeater rollcall`.
- On `rollcall`, while `autorepeat` is `true` and either `count == 'Forever'` or `count > 0`, dispatches `windower.send_command(line)` and schedules the next iteration via `windower.send_command('@wait '..repeatdelay..';repeater rollcall')`, decrementing `count` when numeric.
- Automatically disables `autorepeat = false` on `load` and `zone change` to prevent unintended command loops across zones.

## Commands & Usage
- `//repeater` or `//repeater status` — Print active state, delay, command, and remaining count.
- `//repeater command <cmd>` (or `cmd <cmd>`) — Set the Windower command to repeat (e.g., `input /lastsynth`).
- `//repeater delay <seconds>` — Set repeat interval (integer seconds).
- `//repeater count <n|Forever>` — Set repeat limit or `Forever`.
- `//repeater on|start|begin|go|enable|resume|engage` — Start repeating.
- `//repeater off|stop|end|quit|pause|disable|disengage` — Stop repeating.
- `//repeater repeat` — Toggle repeating on/off.
- `//repeater reload` / `//repeater unload` / `//repeater help`

## Events, Packets & Technical Hooks
- **Windower Events:** `addon command`, `load`, `zone change`
- **Packets:** None (`packets` and `chat`/`chat.chars` are required at top of file but unused)
- **Dependencies / Libraries:** `luau`, `chat`, `chat.chars`, `packets`

## Local Settings & Customizations
- Cloned from `Selindrile/Repeater`; no `data/settings.xml` or local edits.

## Related Notes
- `FFXI Windower Overview`
- `FFXI Windower Addons Catalog`
