# Text-to-Speech Studio (Voilá + ipywidgets)

Generate clear speech from text or PDFs, fine-tune pronunciations, preview samples, and export a ZIP of audio clips—right from a Jupyter/Voilá app.

> Built with **ipywidgets**, **Voilá**, **OpenAI TTS**, and **PyPDF2**.

---

## ✨ Features

* **Two inputs:** type/paste text or upload a **PDF** (auto-extract text).
* **Speaker detection (optional):**

  * `Alice: Hello there` **or** `[Alice] Hello there`.
  * Per-speaker **voice assignment** (saved for the Studio).
* **Pronunciation Library:** CSV-backed dictionary; add/overwrite entries quickly.
* **Voice previews & A/B compare** (uses OpenAI TTS).
* **Sample first:** hear the first **3** lines before generating everything.
* **Full export:** ZIP with:

  * per-line WAVs (or a single **full\_document.wav** when possible),
  * `manifest.csv`, `usage.json`, snapshot of `pronunciations.csv`,
  * original `input_text.txt`, and a small README.
* **Pricing estimates** (optional env vars).
* Clean, responsive UI with a “Speakers” tab and collapsible sidebar.

---

## 📦 Project Structure

```
TTS/
├─ TTSNotebook1.ipynb           # Your main notebook (Voilá entry)
├─ requirements.txt
├─ api.env.example              # Sample env file (no secrets)
├─ .gitignore
├─ README.md
└─ (runtime folders created on first run)
   ├─ samples/                  # temp previews + voice_previews/
   └─ clips/                    # final rendered clips & full_document.wav
```

> The app auto-creates `samples/`, `samples/voice_previews/`, and `clips/` locally. Keep them **git-ignored**.

---

## 🛠️ Prerequisites

* Python **3.10+**
* An **OpenAI API key** with TTS access
* (Recommended) A virtual environment

---

## ⚙️ Setup

1. **Clone** your repo and enter it:

   ```bash
   git clone https://github.com/<you>/TTS.git
   cd TTS
   ```

2. **Create & activate** a virtual env:

   ```bash
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # macOS/Linux
   source .venv/bin/activate
   ```

3. **Install** dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. **Create your env file** (don’t commit secrets):

   * Copy `api.env.example` → `api.env` and fill in:

     ```
     OPENAI_API_KEY=sk-...
     # Optional pricing inputs for estimates (numbers only)
     TTS_PRICE_PER_1K_TOKENS=0.0
     TTS_SECS_PER_TOKEN_EST=0.22
     HUMAN_VO_RATE_PER_FINISHED_MIN=0.0
     # Optional defaults
     OPENAI_TTS_VOICE=alloy
     OPENAI_TTS_MODEL=gpt-4o-mini-tts
     ```

---

## 🚀 Run (recommended)

Launch with **Voilá** for the intended UI:

```bash
voila TTSNotebook1.ipynb
```

By default Voilá serves at `http://localhost:8866/`.

> Running the notebook *inside* Jupyter (without Voilá) will look different because the app applies custom CSS and hides Jupyter chrome for Voilá.

---

## 🧭 Usage

**Home → Enter Studio**

1. **Choose input**

   * **Use text box** – each non-empty line → one clip.
   * **Use PDF** – text auto-extracted (long lines get chunked).
2. *(Optional)* **Speakers**

   * Style: **Single**, **NAME:** prefix, or **\[Name]** bracket.
   * Click **Detect**, assign voices per speaker, **Save**.
3. **Preview**

   * Click **Generate Audio** → hear first **3** lines.
4. **Approve**

   * “Sounds good!” → renders all clips and offers a **ZIP** download.

**Pronunciation Library**

* Add entries (“Original” → “Phonetic”) and **Save**.
* You’ll be asked to **Regenerate samples** to hear the changes.
* File persisted as `pronunciations.csv` at repo root (plus demo terms when demo mode is active).

**Voices**

* Preview voices; **Use** sets the default for Studio.
* A/B compare helper included.

---

## 📄 Files the app creates

* `pronunciations.csv` – your dictionary (persisted).
* `samples/` – temporary sample WAVs and `samples/voice_previews/`.
* `clips/` – final per-line WAVs and **full\_document.wav** when possible.
* ZIP bundle (download only; not saved on disk by default).

Ensure these are **ignored** in `.gitignore`, e.g.:

```
# local runtime
clips/
samples/
*.zip
pronunciations.csv
api.env
.venv/
.ipynb_checkpoints/
```

---

## 🔐 Security

* Keep `api.env` **out of git**.
* If you fork/share the repo, include only `api.env.example`.
* Rotate your API key if it leaks.

---

## 💵 Pricing Estimates (optional)

Set these in `api.env` to see estimates in the UI:

```
TTS_PRICE_PER_1K_TOKENS=0.015   # example
TTS_SECS_PER_TOKEN_EST=0.22     # rendering speed estimate
HUMAN_VO_RATE_PER_FINISHED_MIN=75
```

Estimates appear under the samples before approval and are also written to `usage.json` inside the ZIP.

---

## 🧰 Troubleshooting

* **Blank/very short audio**
  Check API key & network; the app retries with gentle backoff. See console for `[TTS ERROR]`.
* **PDF text missing/garbled**
  PDF may be image-based; extract with OCR first (e.g., Tesseract) and paste text.
* **Widgets look wrong in Jupyter**
  Use **Voilá** (`voila TTSNotebook1.ipynb`) for the intended UI.
* **CORS / static content in corporate environments**
  Serve via a local browser or reverse proxy that permits WebSocket and range requests.

---

## ☁️ Databricks (high-level)

* Upload repo to **Databricks Repos** or workspace.
* On a cluster:

  ```python
  %pip install -r /Workspace/Repos/<you>/TTS/requirements.txt
  ```
* Set env vars via **Cluster → Advanced Options → Environment variables** or **Databricks Secrets** and load them in `api.env` (or adjust the notebook to read from env directly).
* Voilá is a web server; for end-users, it’s often easier to:

  * run this app on a small VM/Container (Voilá) and
  * call **OpenAI** and your **Databricks**/sandbox APIs from there.

> Databricks “Serving Endpoints” are great for APIs; interactive Voilá UIs generally run outside the cluster and call into DB via REST/SQL/Unity endpoints.

---

## 🧪 Dev Tips

* Clear temp audio before a new run if needed:

  ```python
  # inside a cell
  import shutil, pathlib
  for p in pathlib.Path("samples").glob("sample_*.wav"): p.unlink(missing_ok=True)
  ```
* Change default voice/model via env or in the notebook:

  ```python
  OPENAI_TTS_VOICE=alloy
  OPENAI_TTS_MODEL=gpt-4o-mini-tts
  ```

---

## 📝 License

This project is licensed under the terms in **LICENSE** (already in your repo).

---

## 🙏 Acknowledgements

* [Voilá](https://voila.readthedocs.io/)
* [ipywidgets](https://ipywidgets.readthedocs.io/)
* [OpenAI](https://platform.openai.com/)
* [PyPDF2](https://pypi.org/project/PyPDF2/)
* The Jupyter ecosystem 💙

---

## 📮 Support

Open an issue or discussion in this repo. If you need help wiring up deployment or CI, add details about your environment and what you’ve tried.
