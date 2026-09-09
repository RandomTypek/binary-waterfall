# <img src="src/binary_waterfall/resources/icon.png" height="20px" alt="Binary Waterfall"/> Binary Waterfall — Frame Lock fork
### A Raw Data Media Player, with an option that makes purpose-built video files play back cleanly

<p align="center"><img src="docs/example.png" width="400px" alt="Running the program on mspaint.exe"/></p>

This is a fork of [nimaid/binary-waterfall](https://github.com/nimaid/binary-waterfall). Everything the original does, it still does — the only change is a new **Frame Lock** checkbox in Video Settings, off by default.

## What Frame Lock is for

Binary Waterfall slides a window of `Height` rows down a file at the speed of the audio playhead. During live playback the position of that window comes from the audio backend, which reports the time with a few milliseconds of jitter. On ordinary files nobody notices. But if a file was built so that its bytes *are* video frames stored back to back, those few milliseconds put the window a few rows off the frame boundary, and the picture rolls vertically like a TV with a broken vertical hold.

Frame Lock snaps the window to a whole number of `Height` rows, so the view always lands on a frame instead of straddling two. Audio is untouched and stays continuous; only the picture stops sliding.

Leave it **off** for normal files — MP3s, executables, anything not built around a frame grid — where snapping just makes the waterfall move in jerky steps instead of flowing.

## Making files that use it

Frame Lock is only useful with files laid out as frames. Two tools that build them:

- **Web converter** — drag a video in, get a file out, no install: [link](https://randomtypek.github.io/bwv_encode/)
- **Corruptor** — a glitch tool that knows which byte is the picture and which three are the sound: [link](https://randomtypek.github.io/bwv_encode/corrupt.html)
- **`bw_encode.py`** — command-line version, needs ffmpeg and numpy

The general recipe: each pixel byte is the low byte of a 32-bit audio sample (colour format `wxxx`, or `rxxxgxxxbxxx` for RGB), the real audio lives in the top three bytes, and the sample rate is chosen so that exactly one frame's worth of rows scrolls past per 1/fps second.

## Downloads

This fork has no prebuilt binaries. Run it from source:

```
pip install -e .
python binary-waterfall.py
```

For the original program, with Windows builds and a PyPI package, go to [nimaid's repository](https://github.com/nimaid/binary-waterfall).

### Python 3.13+

Two upstream dependencies have drifted. This fork pins them in `pyproject.toml`, so a fresh install handles it:

- `audioop` was removed from the standard library in Python 3.13, and pydub still needs it — supplied by `audioop-lts`
- `moviepy` 2.x dropped the `moviepy.editor` namespace — pinned to `moviepy<2`

## Attribution

Attribution is required for anything you make with this program, for-profit or not, and points at the original project. Reproduce this in your video description or project references:

```
Made with the help of Binary Waterfall:
https://github.com/nimaid/binary-waterfall
```

## Keyboard shortcuts

| Action | Key |
| --- | --- |
| Play / Pause | `Spacebar` |
| Back / Forward | `←` / `→` |
| Frame back / forward | `,` / `.` |
| Restart | `R` |
| Volume up / down | `↑` / `↓` |
| Mute | `M` |

## License

GPL-3.0, same as upstream. Original program by Ella Jameson (nimaid). This fork adds the Frame Lock option in `generators.py`, `dialogs.py`, `window.py` and `constants/defaults.py`; everything else is unmodified.
