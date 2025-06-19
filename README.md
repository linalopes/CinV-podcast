# 🎙️ CinV Podcast Transcription Pipeline

A comprehensive workflow for transcribing WhatsApp audio messages using OpenAI's Whisper model, with speaker identification and text-to-speech capabilities.

## 📋 Project Overview

This project provides an automated pipeline for processing podcast-style audio recordings from WhatsApp voice messages. It includes transcription, speaker identification, audio format conversion, and text-to-speech synthesis capabilities.

### ✨ Features

- 🎯 **Speaker Identification**: Automatic labeling of speakers using CSV mapping
- 🔄 **Batch Processing**: Process multiple audio files with resume capability
- 📝 **Multiple Output Formats**: Individual transcriptions and combined transcripts
- 🎧 **Audio Conversion**: Convert .opus files to .wav for external tools
- 🤖 **Text-to-Speech**: Generate audio from transcriptions using OpenAI and ElevenLabs
- 📊 **Progress Tracking**: Real-time progress bars and status reporting
- 🔐 **Secure API Management**: Environment variables for API keys

## 🗂️ Project Structure

```
CinV-podcast/
├── whatsapp/                    # Source .opus files from WhatsApp
├── txt/                        # Individual transcription outputs
├── wav48/                      # Converted WAV files (48kHz mono)
├── speakers.csv                # Speaker ID mapping
├── combined_transcript.txt     # Final combined transcript
├── transcription.ipynb         # Main transcription notebook
├── requirements.txt            # Python dependencies
├── .gitignore                  # Git ignore rules
└── README.md                   # This file
```

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- FFmpeg (for audio conversion)
- OpenAI API key (for TTS)
- ElevenLabs API key (for voice cloning)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/linalopes/CinV-podcast.git
   cd CinV-podcast
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   ```bash
   # Create .env file from template
   cp env_template.txt .env

   # Edit .env with your API keys
   nano .env
   ```

4. **Prepare your audio files**
   - Place `.opus` files in the `whatsapp/` directory
   - Update `speakers.csv` with speaker mappings

5. **Run the transcription**
   ```bash
   jupyter lab transcription.ipynb
   ```

## ⚙️ Configuration

The project uses a centralized configuration system in the notebook:

```python
CONFIG = {
    "audio_dir": Path("whatsapp"),
    "output_dir": Path("txt"),
    "speakers_csv": Path("speakers.csv"),
    "whisper_model": "medium",   # tiny/base/small/medium/large
    "language": "pt",            # Target language
    "device": "cpu",             # cpu/gpu/mps
}
```

### Whisper Model Options

| Model | Parameters | Speed | Accuracy | Use Case |
|-------|------------|-------|----------|----------|
| `tiny` | 39M | Fastest | Basic | Quick testing |
| `base` | 74M | Fast | Good | General use |
| `small` | 244M | Medium | Better | Balanced |
| `medium` | 769M | Slower | High | ⭐ **Recommended** |
| `large` | 1550M | Slowest | Best | Maximum accuracy |

## 📝 Speaker Configuration

Create a `speakers.csv` file to map audio files to speakers:

```csv
file_id,speaker_name
00000002-AUDIO-2025-06-08-12-31-32,LINA
00000004-AUDIO-2025-06-08-15-43-08,EDU
```

## 🔐 Environment Variables

Create a `.env` file with your API keys:

```env
# OpenAI API Key for TTS
OPENAI_API_KEY=your_openai_api_key_here

# ElevenLabs API Key for voice cloning
ELEVENLABS_API_KEY=your_elevenlabs_api_key_here
```

## 🎤 Workflow

1. **Audio Processing**: Convert WhatsApp .opus files to WAV format
2. **Transcription**: Use Whisper to transcribe audio with speaker labels
3. **Combination**: Merge individual transcriptions into a single file
4. **TTS Generation**: Create audio versions using AI voices (optional)

## 📊 Output Files

- **Individual transcriptions**: `txt/{file_id}_{speaker}.txt`
- **Combined transcript**: `combined_transcript.txt`
- **Converted audio**: `wav48/{file_id}.wav`

## 🛠️ Dependencies

### Core Dependencies
- `torch==2.2.0` - PyTorch backend
- `openai-whisper==20231106` - Speech recognition
- `pandas==2.2.2` - Data manipulation
- `tqdm==4.66.4` - Progress bars

### Audio Processing
- `ffmpeg-python==0.2.0` - Audio conversion
- `pydub==0.25.1` - Audio manipulation
- `soundfile==0.13.1` - Audio file I/O
- `libsndfile==1.2.2` - Audio format support

### Environment Management
- `python-dotenv==1.0.0` - Environment variables

## 🔧 Troubleshooting

### Common Issues

**Model Loading Errors**
- Ensure sufficient disk space for model download
- Check internet connection for first-time downloads
- Verify PyTorch installation

**Audio Processing Issues**
- Verify .opus files are not corrupted
- Check file permissions and paths
- Ensure FFmpeg is installed

**API Key Issues**
- Verify keys are correct in .env file
- Check if keys have expired
- Ensure sufficient credits/quota

### Performance Tips

- Use GPU acceleration when available
- Choose appropriate Whisper model size
- Process during off-peak hours
- Monitor system resources

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [OpenAI Whisper](https://github.com/openai/whisper) for speech recognition
- [ElevenLabs](https://elevenlabs.io/) for voice cloning
- [FFmpeg](https://ffmpeg.org/) for audio processing

## 📞 Support

For questions or issues, please open an issue on GitHub or contact the maintainers.

---

**Note**: This project is designed for Portuguese language audio but can be adapted for other languages by changing the `language` parameter in the configuration.
