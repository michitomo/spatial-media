# Spatial Media Metadata Injector - Standalone Usage

This standalone script provides a cross-platform command-line tool for examining and injecting spatial media metadata (360° video and spatial audio) into MP4/MOV files.

## Why This Script?

The original pre-built binary doesn't run on Apple Silicon Macs (and potentially other modern platforms). This Python script works on **any platform** that has Python 3 installed, including:

- **macOS** (Intel and Apple Silicon)
- **Windows**
- **Linux**
- Any other platform with Python 3

No binary compilation required!

## Prerequisites

You only need **Python 3** installed on your system. No additional dependencies are required for basic metadata injection.

### Check if Python 3 is installed:

```bash
python3 --version
```

If Python 3 is not installed, download it from [python.org](https://www.python.org/downloads/).

## Usage

The script is called `spatial-media-inject` and can be run directly from the repository root.

### Make the script executable (macOS/Linux):

```bash
chmod +x spatial-media-inject
```

### Basic Commands

#### 1. Examine metadata in a video file:

```bash
./spatial-media-inject video.mp4
```

or on Windows:

```bash
python3 spatial-media-inject video.mp4
```

This will print any existing spatial media metadata in the file.

#### 2. Inject 360° equirectangular video metadata:

```bash
./spatial-media-inject -i --projection equirectangular input.mp4 output.mp4
```

This creates a new file `output.mp4` with 360° metadata injected.

#### 3. Inject 360° video with stereo (3D):

**Top-Bottom stereo:**
```bash
./spatial-media-inject -i --projection equirectangular --stereo top-bottom input.mp4 output.mp4
```

**Left-Right stereo:**
```bash
./spatial-media-inject -i --projection equirectangular --stereo left-right input.mp4 output.mp4
```

#### 4. Inject spatial audio metadata:

```bash
./spatial-media-inject -i --spatial-audio input.mp4 output.mp4
```

Note: The file must contain a 4-channel first-order ambisonics audio track with ACN channel ordering and SN3D normalization.

#### 5. Use v2 metadata specification:

```bash
./spatial-media-inject -i --v2 --projection equirectangular input.mp4 output.mp4
```

The v2 specification is newer and recommended for modern 360° video applications.

#### 6. Inject metadata with crop parameters:

```bash
./spatial-media-inject -i --projection equirectangular --crop "1920:1080:3840:2160:0:0" input.mp4 output.mp4
```

Crop format: `w:h:f_w:f_h:x:y` where:
- `w` = CroppedAreaImageWidthPixels
- `h` = CroppedAreaImageHeightPixels
- `f_w` = FullPanoWidthPixels
- `f_h` = FullPanoHeightPixels
- `x` = CroppedAreaLeftPixels
- `y` = CroppedAreaTopPixels

### Command-Line Options

```
usage: spatial-media-inject [options] [files...]

positional arguments:
  file                  input/output files

options:
  -h, --help            show this help message and exit
  -i, --inject          injects spatial media metadata into the first file
                        specified (.mp4 or .mov) and saves the result to the
                        second file specified
  -2, --v2              Uses v2 of the video metadata spec

Spherical Video:
  -s STEREO-MODE, --stereo STEREO-MODE
                        stereo mode (none | top-bottom | left-right)
  -p {none,equirectangular}, --projection {none,equirectangular}
                        projection (none | equirectangular)
  -c CROP, --crop CROP  crop region. Must specify 6 integers in the form of
                        "w:h:f_w:f_h:x:y"
  -b BOUNDS, --bounds BOUNDS
                        Equirect projection bounds for VR180

Spatial Audio:
  -a, --spatial-audio   spatial audio. First-order periphonic ambisonics with
                        ACN channel ordering and SN3D normalization
```

## Examples

### Example 1: Convert a standard video to 360° equirectangular

```bash
./spatial-media-inject -i --projection equirectangular my-360-video.mp4 my-360-video-spatial.mp4
```

After injection, `my-360-video-spatial.mp4` will be recognized as a 360° video by players like YouTube, Facebook, and VR headsets.

### Example 2: Check metadata in a file

```bash
./spatial-media-inject my-360-video-spatial.mp4
```

Output:
```
Processing: my-360-video-spatial.mp4
Loaded file...
	Track 0
		Spherical = true
		Stitched = true
		StitchingSoftware = Spherical Metadata Tool
		ProjectionType = equirectangular
```

### Example 3: Add both video and audio spatial metadata

```bash
./spatial-media-inject -i --projection equirectangular --spatial-audio input.mp4 output.mp4
```

## Supported File Formats

- MP4 (`.mp4`)
- QuickTime MOV (`.mov`)

## What This Tool Does

The Spatial Media Metadata Injector adds special metadata to video files that tells players and VR applications how to properly display 360° videos and spatial audio. This includes:

### For Spherical/360° Video:
- Projection type (equirectangular)
- Stereo mode (mono, top-bottom, left-right)
- Crop parameters for partial panoramas
- VR180 projection bounds

### For Spatial Audio:
- Ambisonic audio metadata
- Channel ordering (ACN)
- Normalization (SN3D)
- Head-locked stereo support

The metadata follows these specifications:
- [Spherical Video RFC](docs/spherical-video-rfc.md)
- [Spherical Video V2 RFC](docs/spherical-video-v2-rfc.md)
- [Spatial Audio RFC](docs/spatial-audio-rfc.md)

## Troubleshooting

### "Permission denied" error (macOS/Linux)

Make the script executable:
```bash
chmod +x spatial-media-inject
```

### Python not found

Make sure Python 3 is installed:
```bash
python3 --version
```

If not installed, download from [python.org](https://www.python.org/downloads/).

### "Input and output cannot be the same"

The tool creates a new file with metadata injected. You must specify different input and output filenames.

## Differences from the Binary

This standalone script:
- ✅ Works on Apple Silicon Macs
- ✅ Works on any platform with Python 3
- ✅ No compilation needed
- ✅ Easy to update and maintain
- ✅ Fully open source
- ❌ No GUI (command-line only)

The original GUI application is still available via `spatialmedia/gui.py` but requires additional dependencies (PyInstaller, tk, Pillow).

## Advanced: Running as a Python Module

If you prefer, you can also run the tool as a Python module:

```bash
python3 -m spatialmedia [options] [files...]
```

This is equivalent to using the standalone script.

## Contributing

This tool is part of the [Spatial Media](https://github.com/google/spatial-media) project. For issues, feature requests, or contributions, please visit the GitHub repository.

## License

Apache License 2.0 - See [LICENSE](LICENSE) file for details.
