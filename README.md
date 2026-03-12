# 🎙️ ArabicVoiceAI — Arabic Speech-to-Summary Pipeline

> **Intelligent Arabic Audio Processing:** Transcribe, Diarize, Clean, Summarize & Speak — End-to-End.

<!-- Banner image -->
<p align="center">
  <img src="assets/banner.png" alt="ArabicVoiceAI Banner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-Python_3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/NLP-Arabic_Processing-06B6D4?style=for-the-badge&logo=nlp&logoColor=white" />
  <img src="https://img.shields.io/badge/ASR-WhisperX-8B5CF6?style=for-the-badge&logo=openai&logoColor=white" />
  <img src="https://img.shields.io/badge/LLM-Gemini_1.5_Flash-F59E0B?style=for-the-badge&logo=google&logoColor=white" />
  <img src="https://img.shields.io/badge/TTS-XTTS-EC4899?style=for-the-badge&logo=soundcloud&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-10B981?style=for-the-badge" />
</p>

---

## 📖 Overview

**ArabicVoiceAI** is a modular NLP pipeline that transforms raw Arabic audio or video files into clean, structured summaries — and reads them back aloud. It seamlessly combines state-of-the-art automatic speech recognition (ASR), multi-speaker diarization, Arabic text normalization, AI-powered summarization (via Google Gemini), and neural text-to-speech synthesis (XTTS).

Whether you're processing interviews, lectures, podcasts, or meeting recordings in Arabic, **ArabicVoiceAI** does the heavy lifting for you.

---

## ✨ Features

- 🎤 **Automatic Speech Recognition** — Supports both Whisper and WhisperX for accurate Arabic transcription
- 👥 **Speaker Diarization** — Identifies and separates multiple speakers in a recording
- 🧹 **Arabic Text Cleaning** — Normalizes and preprocesses Arabic transcripts (diacritics, punctuation, encoding)
- 🤖 **AI Summarization** — Leverages Google Gemini 1.5 Flash for concise, intelligent summaries
- 🔊 **Text-to-Speech** — Synthesizes the summary back to audio using XTTS neural TTS
- 🔄 **Modular Architecture** — Each stage is an independent, reusable Python module
- ⚡ **CLI-First Design** — Run the full pipeline from a single command

---

## 🏗️ Project Architecture

```
NLP_PROJECT/
├── Transcript and summarization/
│   ├── main.py                        ← 🎯 Pipeline orchestrator (CLI entry point)
│   ├── transcription_and_diarization.py  ← 🎤 ASR + speaker diarization
│   ├── cleaning_preprocessing.py      ← 🧹 Arabic text normalization & cleanup
│   ├── summarization_google.py        ← 🤖 Gemini-powered summarization
│   ├── text_to_speech.py              ← 🔊 XTTS Arabic TTS synthesis
│   └── requirements.txt               ← 📦 Python dependencies
└── README.md                          ← 📄 This file
```

---

## 🧩 Module Overview

| Module | Purpose | Key Technologies |
|--------|---------|-----------------|
| `transcription_and_diarization.py` | Loads audio/video, runs ASR, performs multi-speaker diarization, returns structured segments | WhisperX, PyAnnote |
| `cleaning_preprocessing.py` | Cleans and normalizes raw Arabic text (diacritics removal, encoding fixes, punctuation) | Regex, Camel-Tools / NLTK |
| `summarization_google.py` | Sends cleaned transcript chunks to Google Gemini and returns a concise Arabic summary | Google Generative AI SDK |
| `text_to_speech.py` | Converts the final Arabic summary text into speech audio | XTTS / Coqui TTS |
| `main.py` | CLI orchestrator that chains all modules together in sequence | argparse |

---

## 🚀 Quick Start

### 1. Clone & Set Up Environment

```bash
git clone https://github.com/your-username/NLP_PROJECT.git
cd NLP_PROJECT

# Create and activate virtual environment
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install -r "Transcript and summarization/requirements.txt"
```

### 3. Configure Google API Credentials

```bash
# Set your Google Cloud credentials
export GOOGLE_APPLICATION_CREDENTIALS="path/to/your/service-account.json"

# Or use API key directly in summarization_google.py
```

### 4. Run the Full Pipeline

```bash
python "Transcript and summarization/main.py" --input your_audio.mp3
```

---

## 🔧 Usage Examples

### Full End-to-End Pipeline (Python API)

```python
from transcription_and_diarization import transcribe_and_diarize
from cleaning_preprocessing import clean_arabic_transcript
from summarization_google import summarize
from text_to_speech import generate_audio

# Step 1: Transcribe & diarize
segments = transcribe_and_diarize("interview.mp3", language="ar")

# Step 2: Join raw text
raw_text = "\n".join([s["text"] for s in segments])

# Step 3: Clean and normalize Arabic text
cleaned = clean_arabic_transcript(raw_text)

# Step 4: Generate summary using Gemini
summary = summarize(cleaned)

# Step 5: Synthesize audio summary
audio_path = generate_audio(summary)
print("✅ Done! Audio summary saved to:", audio_path)
```

### CLI Usage

```bash
# Process a local audio file
python main.py --input path/to/interview.mp3

# Expected output:
# ✅ Success! Audio summary saved to output_summary.wav
```

---

## 🔄 Pipeline Flow

```
Audio / Video File
        │
        ▼
┌──────────────────────┐
│  ASR + Diarization   │  ← WhisperX + PyAnnote
│  (per-speaker segs.) │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  Arabic Text Cleanup │  ← Normalization, encoding fix
│  & Preprocessing     │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  Summarization       │  ← Google Gemini 1.5 Flash
│  (Gemini LLM)        │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  Text-to-Speech      │  ← XTTS (Arabic TTS)
│  Audio Output        │
└──────────────────────┘
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `whisperx` | latest | Arabic ASR + alignment |
| `google-generativeai` | latest | Gemini summarization |
| `TTS` (Coqui) | latest | XTTS Arabic speech synthesis |
| `pyannote.audio` | latest | Speaker diarization |
| `torch` | ≥2.0 | Deep learning backend |
| `transformers` | latest | Hugging Face model support |

Install all at once:
```bash
pip install -r requirements.txt
```

---

## 🛠️ Development & Contribution

1. **Fork** the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Make your changes and add tests
4. Commit: `git commit -m "feat: add my feature"`
5. Push: `git push origin feature/my-feature`
6. Open a **Pull Request**

---

## 🗺️ Roadmap

- [ ] Implement `transcription_and_diarization.py` with WhisperX
- [ ] Implement `summarization_google.py` with Gemini 1.5 Flash
- [ ] Implement `text_to_speech.py` with XTTS Arabic model
- [ ] Add Gradio web interface
- [ ] Support batch processing of multiple files
- [ ] Add confidence scoring for transcription segments
- [ ] Dockerize the pipeline

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- [OpenAI Whisper](https://github.com/openai/whisper) & [WhisperX](https://github.com/m-bain/whisperX) for Arabic ASR
- [Google Gemini](https://ai.google.dev/) for intelligent summarization
- [Coqui TTS / XTTS](https://github.com/coqui-ai/TTS) for Arabic voice synthesis
- [PyAnnote Audio](https://github.com/pyannote/pyannote-audio) for speaker diarization

---

<p align="center">
  Made with ❤️ for Arabic NLP · <strong>ArabicVoiceAI</strong>
</p>
