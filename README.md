# Video_to_Standard-Operating-Procedure_SOP

**Automatically convert training videos into professional Standard Operating Procedure (SOP) manuals using AI.**

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-brightgreen)

---

## Table of Contents

- [Overview](#overview)
- [Highlights](#highlights)
- [Features](#features)
- [Performance](#performance)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Output](#output)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)
- [Use Cases](#use-cases)
- [Limitations](#limitations)
- [Roadmap](#roadmap)
- [Dependencies](#dependencies)
- [License](#license)
- [Support](#support)

---

## Overview

**Video_to_Standard-Operating-Procedure_SOP** is a tool that uses multimodal AI and speech-to-text transcription to analyze industrial and manufacturing training videos and automatically generate step-by-step SOP manuals with embedded screenshots.

It supports two execution modes:

- **Local Mode** — Runs entirely on local hardware using a GPU-based vision model and transcription engine, for privacy and zero ongoing API cost.
- **API Mode** — Uses cloud-based AI services, for users without dedicated GPU hardware.

## Highlights

| | |
|---|---|
| 🚀 **Local GPU Mode** | Run the full pipeline on your own hardware with no cloud dependency |
| ⚡ **Fast Frame Extraction** | FFmpeg-powered extraction, significantly faster than traditional methods |
| 🎯 **Accurate Transcription** | Timestamped audio transcription cross-referenced with video frames |
| ✅ **Complete Procedures** | Covers disassembly, repair, reassembly, and verification steps |
| 📊 **Performance Timing** | Displays a processing-time breakdown for each pipeline phase |
| 🧹 **Auto Cleanup** | Temporary frames are removed automatically after generation |
| 💸 **Zero Cost Option** | No API fees when running fully in Local Mode |

## Features

- **Fast Video Processing** — FFmpeg-based key frame extraction
- **Hybrid Audio Transcription** — Local (GPU-based) or cloud-based speech-to-text
- **Hybrid Vision Analysis** — Local vision-language model or cloud multimodal AI
- **Professional PDFs** — Polished SOP manuals with embedded images and clear instructions
- **Fast Turnaround** — A short training video can be converted to a full SOP in under two minutes
- **Safety Notes** — Safety considerations are identified automatically
- **Full Procedure Coverage** — From setup through final verification

## Performance

Reference timings for a typical short training video:

| Operation | API Mode | Local GPU Mode |
|---|---|---|
| Transcription | ~30s | ~5s |
| Frame Extraction | ~8s | ~8s |
| AI Analysis | ~75s | ~20s |
| PDF Generation | ~5s | ~5s |
| **Total Time** | **~2 minutes** | **~40 seconds** |
| **Cost per video** | Small per-call fee | **$0.00** |

*Actual timing depends on video length, hardware, and network conditions.*

## Installation

### Prerequisites

- Python 3.8+ (Windows/Linux)
- FFmpeg — see the platform setup guide included in this repository
- **Local Mode:** An NVIDIA GPU, a local model-serving backend, and a local transcription engine
  - A GPU detection script is included to recommend a model size based on available VRAM
- **API Mode:** API keys for a cloud multimodal AI provider and a cloud transcription provider

### Quick Setup

```bash
# Clone the repository
git clone https://github.com/<your-username>/Video_to_Standard-Operating-Procedure_SOP.git
cd Video_to_Standard-Operating-Procedure_SOP

# Run the automated setup script for your platform
./setup_linux.sh          # Linux
# or
.\setup_windows.ps1        # Windows
```

The setup script will:
- Detect an available GPU, if present
- Install all dependencies (FFmpeg, Python packages, local AI runtime)
- Recommend an AI model based on available VRAM
- Download the vision model, if selected
- Create a `.env` configuration file

### Manual Setup

For manual installation steps on both platforms, see the platform setup guide included in this repository.

## Configuration

After setup, edit the `.env` file:

**Local Mode**
```ini
AI_MODE=LOCAL
VISION_MODEL=              # Leave empty for auto-detection
TRANSCRIPTION_MODEL=       # Leave empty for auto-detection
```

**API Mode**
```ini
AI_MODE=API
VISION_API_KEY=your_key_here
TRANSCRIPTION_API_KEY=your_key_here
```

## Usage

### Basic

```bash
python main.py path/to/video.mp4
```

This will:
1. Extract audio and generate a timestamped transcript
2. Extract key frames from the video
3. Analyze the content with AI to generate a complete procedure
4. Generate a professional PDF
5. Automatically clean up temporary files

### Advanced

```bash
python main.py video.mp4 \
  --output my_sop.pdf \
  --context "Task description, e.g. Car Tire Repair and Replacement" \
  --company "Your Company Name"
```

### Command-Line Options

| Option | Description | Default |
|---|---|---|
| `video` | Path to input video file | *(required)* |
| `-o, --output` | Output PDF filename | `output_sop.pdf` |
| `-c, --context` | Task context for better analysis | Auto-detected |
| `--company` | Company name for PDF header | `"Your Company"` |

## How It Works

```
Video Input → Audio Transcription → Frame Extraction → AI Analysis → PDF Generation → Cleanup
```

1. **Audio Transcription** — Extracts audio and transcribes it into timestamped segments, providing context for matching spoken instructions to the correct frames.
2. **Frame Extraction** — Extracts key frames at set intervals (default: every 2 seconds) and resizes them for efficient AI processing, preserving timestamp information.
3. **AI Analysis** — Cross-references audio and frame timestamps to build a structured procedure, returned as JSON with steps, safety notes, and reasoning. Runs on a local model or a cloud API depending on configuration.
4. **PDF Generation** — Assembles a professional document with embedded images, safety notes, a table of contents, headers, and page numbers.
5. **Automatic Cleanup** — Deletes temporary extracted frames after PDF generation, keeping only the final output.

## Output

Every generated SOP includes:

- **Cover Page** — Title page with company branding
- **Table of Contents** — Easy navigation to all sections
- **Safety Section** — Automatically identified safety considerations
- **Step-by-Step Instructions** — Numbered steps with timestamp references, corresponding images, and notes for each step
- **Complete Procedures** — Disassembly, repair/maintenance, reassembly, and final verification and testing

## Project Structure

```
Video_to_Standard-Operating-Procedure_SOP/
├── main.py                 # Main application entry point
├── video_processor.py      # Frame extraction (FFmpeg)
├── sop_analyzer.py         # AI analysis
├── transcription.py        # Audio transcription
├── pdf_generator.py        # PDF creation
├── requirements.txt        # Dependencies
├── .env.example             # Configuration template
├── example_output/          # Sample output PDF
└── README.md                 # Project documentation
```

## Troubleshooting

**API key not found**
Confirm you created a `.env` file (not `.env.example`) and that the key is valid.

**Import errors for computer-vision libraries**
```bash
pip install opencv-python
```

**Video processing fails**
- Check the video format (MP4 and MOV are supported)
- Ensure the video file is not corrupted
- Try a shorter video first

**PDF generation fails**
```bash
pip install reportlab
```
Also check available disk space for the output file.

## Use Cases

- Manufacturing and industrial training documentation
- Safety compliance and audit-ready procedures
- Equipment setup, maintenance, and repair guides
- Standardizing training material across teams and locations

## Limitations

- Output quality depends on video clarity and lighting
- Works best with a stable camera angle
- Currently optimized for English (adaptable to other languages)
- Processing time scales with video length

## Roadmap

- [x] Web interface
- [ ] Multi-language support
- [ ] Video quality validation
- [ ] Custom branding options
- [ ] Step editing interface
- [ ] Voice narration support
- [ ] Additional video format support
- [ ] Batch processing

## Dependencies

- Video frame extraction and processing (OpenCV, FFmpeg)
- Multimodal AI analysis (local or cloud)
- PDF generation (ReportLab)
- Image processing (Pillow)
- Environment configuration (python-dotenv)

## License

This project is available for educational and commercial use under the MIT License.

## Support

For questions or issues:
1. Check this README
2. Review the code comments in the source files
3. Consult the relevant API documentation for your configured AI backend
