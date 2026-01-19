# Spatial Media

A collection of specifications and tools for 360&deg; video and spatial audio, including:

- [Spatial Audio](docs/spatial-audio-rfc.md) metadata specification
- [Spherical Video](docs/spherical-video-rfc.md) metadata specification
- [Spherical Video V2](docs/spherical-video-v2-rfc.md) metadata specification
- [VR180 Video Format](docs/vr180.md) VR180 video format
- [Spatial Media tools](spatialmedia/) for injecting spatial media metadata in media files

## Cross-Platform Standalone Tool

**NEW: Works on Apple Silicon and all platforms!**

We now provide a standalone command-line script that works on any platform with Python 3, including Apple Silicon Macs, Intel Macs, Windows, and Linux. No binary compilation required!

### Quick Start

```bash
# Make executable (macOS/Linux)
chmod +x spatial-media-inject

# Examine metadata in a video
./spatial-media-inject video.mp4

# Inject 360° metadata
./spatial-media-inject -i --projection equirectangular input.mp4 output.mp4

# On Windows
python3 spatial-media-inject video.mp4
```

**📖 [Full Usage Guide](STANDALONE_USAGE.md)** - Complete documentation with examples

### Why Use the Standalone Script?

- ✅ **Works on Apple Silicon** - No compatibility issues
- ✅ **Cross-platform** - macOS, Windows, Linux
- ✅ **No build required** - Just Python 3
- ✅ **Simple to use** - Command-line interface
- ✅ **Always up-to-date** - No need to wait for binary releases
