# <img src="https://github.com/nimaid/binary-waterfall/blob/main/src/binary_waterfall/resources/icon.png?raw=true" height="20px" alt="Binary Waterfall"/> Binary Waterfall — Frame Lock fork
### A Raw Data Media Player, with an option that makes purpose-built video files play back cleanly

<p align="center"><img src="https://github.com/nimaid/binary-waterfall/blob/main/docs/example.png?raw=true" width="400px" alt="Running the program on mspaint.exe"/></p>

A fork of [nimaid/binary-waterfall](https://github.com/nimaid/binary-waterfall). Everything the original does, it still does — the only change is a new **Frame Lock** checkbox in Video Settings, off by default.

## Frame Lock

Binary Waterfall slides a window of `Height` rows down a file at the speed of the audio playhead. During live playback that position comes from the audio backend, which reports the time with a few milliseconds of jitter. On ordinary files nobody notices. But if a file was built so that its bytes *are* video frames stored back to back, those milliseconds put the window a few rows off the frame boundary and the picture rolls vertically.

Frame Lock snaps the window to a whole number of `Height` rows, so the view always lands on a frame instead of straddling two. Audio is untouched. Leave it off for normal files, where snapping only makes the waterfall move in jerky steps.

## Command Line Usage
After installing the module, run `binary-waterfall`.

## Attribution
If you use this program to make a video or other project, you must provide attribution. Attribution is required regardless of whether your project is for-profit or not. Please reproduce the following attribution statement in full in your video description or otherwise include it in the references for your project:
```
Made with the help of Binary Waterfall:
https://github.com/nimaid/binary-waterfall
```

## Keyboard Shortcuts
- **Play / Pause:** `Spacebar`
- **Back:** `Left Arrow`
- **Forward:** `Right Arrow`
- **Frame Back:** `<` (`,`)
- **Frame Forward:** `>` (`.`)
- **Restart:** `R`
- **Volume Up:** `Up Arrow`
- **Volume Down:** `Down Arrow`
- **Mute / Unmute:** `M`

## License
GPL-3.0, same as upstream. Original program by Ella Jameson (nimaid); this fork adds the Frame Lock option.
