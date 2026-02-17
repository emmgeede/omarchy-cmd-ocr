# omarchy-cmd-ocr

CleanShot X-style OCR text capture for Hyprland. Select a screen region and the recognized text is copied to your clipboard. Designed for [Omarchy](https://github.com/basecamp/omarchy).

## Install

```bash
yay -S omarchy-cmd-ocr
```

Or build manually:

```bash
git clone https://aur.archlinux.org/omarchy-cmd-ocr.git
cd omarchy-cmd-ocr
makepkg -si
```

## Setup

Add this line to your Hyprland config (e.g. `~/.config/hypr/hyprland.conf`):

```conf
source = /usr/share/omarchy-cmd-ocr/hyprland-bindings.conf
```

The default keybindings use `SUPER+ALT+O` / `SUPER+ALT+SHIFT+O`. To use different modifiers, copy and edit:

```bash
cp /usr/share/omarchy-cmd-ocr/hyprland-bindings.conf ~/.config/hypr/ocr-bindings.conf
# Edit to taste, then source your local copy instead
```

## Usage

| Action | Default Binding | Command |
|--------|----------------|---------|
| OCR (formatted) | `Super+Alt+O` | `omarchy-cmd-ocr` |
| OCR (compact) | `Super+Alt+Shift+O` | `omarchy-cmd-ocr compact` |

**Formatted** mode preserves the original text layout. **Compact** mode joins all lines and collapses whitespace into a single line.

## How it works

1. Screen freezes via `wayfreeze`
2. Select a region or window with `slurp` (same smart selection as Omarchy screenshots)
3. `grim` captures the region, pipes to `tesseract` for OCR
4. Recognized text is copied to clipboard via `wl-copy`
5. A notification shows a preview of the captured text

## Dependencies

- `tesseract` + `tesseract-data-eng` — OCR engine
- `grim` — screenshot capture
- `slurp` — region selection
- `wayfreeze` — screen freeze during selection
- `wl-clipboard` — clipboard access
- `jq` — JSON parsing for monitor/window geometry
- `libnotify` — desktop notifications
- `hyprland` — window manager (for `hyprctl`)

## License

MIT
