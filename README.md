# X11 Mic Monitor

Hear your own microphone on a mouse button, or record yourself and hear it straight back. X11 + PipeWire.

| Press              | Result                                          |
| ------------------ | ----------------------------------------------- |
| `Mouse5`           | hear yourself, half a second late               |
| `Mouse5 + Mouse4`  | hear yourself with no delay                     |
| `Windows + Mouse5` | record while held, play it back when you let go |

## Parts

| File          | Purpose                                                 |
| ------------- | ------------------------------------------------------- |
| `mic-monitor` | The whole thing                                         |
| `install`     | Copies it to `~/.local/bin`, starts it now and at login |

## Requirements

- Linux
- X11
- PipeWire and its tools: `pw-loopback`, `pw-record`, `pw-play`
- Python 3
- libX11, libXi and libXtst

## Install

```sh
./install
./install --dry-run
```

## Settings

At the top of `mic-monitor`. Run `./install` again afterwards; it replaces the running copy.

| Setting      | Default  | Meaning                                                            |
| ------------ | -------- | ------------------------------------------------------------------ |
| `MODE`       | `"hold"` | `"hold"`: on while Mouse5 is held. `"toggle"`: each press switches |
| `DELAY`      | `0.5`    | Seconds late you hear yourself; Mouse4 with Mouse5 skips it        |
| `LATENCY_MS` | `2`      | Latency asked for with no delay; raise it if that crackles         |

## Behaviour

| What                          | How                                                                                    |
| ----------------------------- | -------------------------------------------------------------------------------------- |
| Other windows                 | never see Mouse5, and while it is held they do not see other buttons either            |
| Fullscreen games              | a game holding the pointer still receives Mouse5; listening works anyway               |
| Mouse4 pressed first          | both buttons reach the window under the pointer; listening works anyway, without delay |
| Letting go                    | playing continues until what you said before has been heard                            |
| Pressing Mouse5 in a playback | stops the playback                                                                     |
| XFCE and the Windows key      | a shortcut bound to Windows alone would fire on release; a blank key tap cancels it    |
| Cost                          | wakes only on mouse buttons; the audio stream exists only while in use                 |
| The recording                 | `$XDG_RUNTIME_DIR/mic-monitor.wav`, until the next one or logout                       |

## Removal

```sh
pkill -f "^python3 $HOME/.local/bin/mic-monitor\$"
rm -f ~/.local/bin/mic-monitor ~/.config/autostart/mic-monitor.desktop
```

## License

MIT [LICENSE](LICENSE)  
By MattFor
