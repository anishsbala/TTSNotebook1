# 🗣️ Text-to-Speech (TTS) Notebook

This project provides an interactive **Text-to-Speech (TTS) system** built in a Jupyter Notebook environment.  
It allows users to input text directly or upload a PDF, split text into smaller segments, generate audio using **gTTS**, and selectively package chosen segments into a downloadable ZIP file.  
The front-end is powered by **ipywidgets**, making it deployable with **Voila** or on platforms like **Databricks**.

---

## 🚀 Features

- **Multiple Input Modes**
  - Type or paste text directly.
  - Upload PDF files and extract text.

- **Automatic Segmentation**
  - Split extracted text into ~3 equal segments for easier playback.
  - Each segment processed separately for modular audio.

- **Audio Generation**
  - Convert each text segment to `.mp3` using [gTTS](https://pypi.org/project/gTTS/).
  - Built-in playback widgets for preview.

- **Selective Export**
  - Use checkboxes to select desired segments.
  - Package selected audio files into a `.zip` with a base64 download link.

- **Interactive UI**
  - Built with `ipywidgets` for toggles, checkboxes, dynamic labels, and download buttons.
  - Designed for use in Jupyter + Voila dashboards.

---

## 📂 Project Structure

TTS/
│── notebooks/
│ └── tts_app.ipynb # Main interactive notebook
│── requirements.txt # Python dependencies
│── README.md # This file
│── LICENSE
│── .gitignore