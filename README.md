# bplayer

**Blazing fast music player** – A unified **mpv** player control script for Arch Linux, featuring Tofi-based menus, Dunst notifications, and seamless playlist management.

## Features

- **Playlist Selection** – Launch mpv with a directory-based playlist selector
- **Playback Controls** – Play/pause, seek, speed adjustment, loop, shuffle, and more
- **Volume Control** – Adjust volume (+/-10%) and mute/unmute
- **Track Switching** – Navigate tracks within the current playlist
- **Rich Notifications** – Album art, track info, and playback status via Dunst
- **IPC Socket Control** – Direct communication with mpv for real-time commands

## Dependencies

- `zsh`
- `mpv`
- `tofi` (menu launcher)
- `dunst` / `dunstify` (notifications)
- `jq` (JSON parsing)
- `playerctl` (media control)

## Installation

1. Clone or copy the `bplayer` script to your preferred location:
   ```bash
   chmod +x bplayer
   sudo mv bplayer /usr/local/bin/bplayer
   ```

2. (Optional) Configure environment variables in your shell config (`~/.zshrc`):
   ```bash
   export BPLAYER_MUSIC_DIR="$HOME/Music"
   export BPLAYER_DEFAULT_IMG="$HOME/Pictures/My-UIs/no-image-found.png"
   ```

## Usage

```bash
bplayer [command]
```

| Command   | Description                                      |
|-----------|--------------------------------------------------|
| `start`   | Launch mpv with playlist selection               |
| `actions` | Show playback control menu                       |
| `select`  | Select a track from the current playlist         |
| `change`  | Change to a different playlist                   |
| `noti`    | Enable playback notifications (run with `&`)     |
| `check`   | Check if mpv is running (exit code 0 if yes)     |
| `stop`    | Stop mpv and clean up socket                     |
| `help`    | Show help message                                |

### Examples

```bash
# Start player with playlist selector
bplayer start

# Open control menu
bplayer actions

# Change playlist (or run `bplayer` with no args when mpv is running)
bplayer change

# Enable notifications (background)
bplayer noti &

# Check mpv status
bplayer check && echo "mpv is running"
```

## Keyboard Integration

Bind commands to your window manager for quick access.

**Hyprland:**
```bash
# ~/.config/hypr/hyprland.conf
exec-once = bplayer noti
bind = SUPER, F1, exec, bplayer start
bind = SUPER, F2, exec, bplayer actions
bind = SUPER, F3, exec, bplayer select
bind = SUPER, F4, exec, bplayer change
```

**Sway/i3:**
```bash
# ~/.config/sway/config
bindsym $mod+F1 exec bplayer start
bindsym $mod+F2 exec bplayer actions
bindsym $mod+F3 exec bplayer select
bindsym $mod+F4 exec bplayer change
```

## Configuration

Configure via **environment variables** (no need to edit the script):

| Variable              | Description                          | Default                                      |
|-----------------------|--------------------------------------|----------------------------------------------|
| `BPLAYER_SOCKET`      | IPC socket path                      | `${XDG_RUNTIME_DIR:-/tmp}/mpvsocket`         |
| `BPLAYER_DEFAULT_IMG` | Fallback notification image          | Script directory's `no-image-found.svg`      |
| `BPLAYER_MUSIC_DIR`   | Music directory for playlist search  | `~/Music`                                    |

### Examples

```bash
# Use XDG-compliant socket path (recommended)
export BPLAYER_SOCKET="$XDG_RUNTIME_DIR/mpvsocket"

# Custom music directory
export BPLAYER_MUSIC_DIR="$HOME/media/music"

# Custom fallback image
export BPLAYER_DEFAULT_IMG="$HOME/.config/bmusic/no-art.png"
```

Add these to your shell config (`~/.zshrc`) for persistence.

## License

Free to use and modify.
