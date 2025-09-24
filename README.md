# 🎙️ Text-to-Speech (TTS) Notebook  

Turn **text or PDF files into audio** with an interactive Jupyter Notebook. Powered by **Google Text-to-Speech (gTTS)** and a user-friendly UI built with **ipywidgets**.  

---

## ✨ Features  
- 📝 **Dual Input Modes**  
  - Enter text directly  
  - Upload PDF for auto-extraction  

- 🔊 **Segmented Conversion**  
  - Splits text into ~3 equal parts  
  - One audio file per segment  

- 📦 **Selective Packaging**  
  - Pick which audio files to keep  
  - Download as a ZIP with a single click  

- 🎛️ **Interactive UI**  
  - Toggle buttons, file upload, checkboxes  
  - Browser-friendly with **Voila**  

---

## 🛠️ Tech Stack  
- **Python**  
- **Jupyter Notebook** / **Voila**  
- **gTTS**  
- **ipywidgets**  
- **PyPDF2**  
- **zipfile** + **base64**  

---

## ⚙️ Installation  

1. Clone the repo:  
   ```bash
   git clone https://github.com/<your-username>/TTS.git
   cd TTS
````

2. Create & activate a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate   # Mac/Linux
   venv\Scripts\activate      # Windows
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

---

## 🚀 Usage

### Run in Jupyter

```bash
jupyter notebook
```

Open `tts_notebook.ipynb` and use the UI.

### Run as Web App

```bash
voila tts_notebook.ipynb
```

Launches a clean web interface (no code visible).

---

## 🔄 Workflow

1. Select input type (**Text** or **PDF**)
2. Upload PDF or enter text
3. Auto-split into segments
4. Generate audio via gTTS
5. Select audio segments
6. Download as a ZIP

---

## 📂 Project Structure

```
TTS/
├── notebooks/
│   └── tts_notebook.ipynb
├── requirements.txt
├── README.md
└── LICENSE
```

---

## 📦 Requirements

Core dependencies:

* `gTTS`
* `ipywidgets`
* `PyPDF2`
* `notebook` + `voila`

See `requirements.txt` for full list.

---

## 📸 Example UI

* Text area for manual input
* PDF file upload widget
* Toggle for input type
* Checkboxes for segment selection
* Auto-generated download links

---

## 📜 License

MIT License. See `LICENSE` for details.

---

## 🚧 Future Enhancements

* Support for multiple TTS providers (Azure, OpenAI)
* Voice, speed, and language customization
* Transcript + audio side-by-side
* Advanced multi-language PDF extraction

