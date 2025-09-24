Text-to-Speech Studio (Voilá + ipywidgets)

Generate speech from text or PDFs, auto-detect speakers, manage a pronunciation dictionary, preview samples, and export a ZIP (clips, manifest, usage).

Requirements

Python 3.10+

OpenAI API key (TTS access)

Quick Setup
# clone & enter
git clone https://github.com/<you>/TTS.git
cd TTS

# venv
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

# install
pip install -r requirements.txt

Configure API

Copy api.env.example → api.env and set:

OPENAI_API_KEY=sk-...
OPENAI_TTS_MODEL=gpt-4o-mini-tts
OPENAI_TTS_VOICE=alloy
# Optional estimates:
TTS_PRICE_PER_1K_TOKENS=0.0
TTS_SECS_PER_TOKEN_EST=0.22
HUMAN_VO_RATE_PER_FINISHED_MIN=0.0

Run (recommended)
voila TTSNotebook1.ipynb


Open the served URL (usually http://localhost:8866/).

Running inside plain Jupyter will look different; Voilá is the intended UI.

How to Use

Choose input: Type/paste text or upload a PDF.

(Optional) Speakers: Use Alice: Hi or [Alice] Hi; click Detect, assign voices, Save.

Generate Audio: Hear first 3 samples.

Approve: Render all clips and download the ZIP (with manifest.csv, usage.json, pronunciations.csv snapshot, and input_text.txt).

Project Layout
TTSNotebook1.ipynb       # main app (Voilá entry)
requirements.txt
api.env.example
README.md
.gitignore
# created at runtime:
samples/                 # previews + voice_previews/
clips/                   # final WAVs + full_document.wav
pronunciations.csv       # your dictionary (persisted)

.gitignore (important)
# env & runtime
api.env
.venv/
.ipynb_checkpoints/
samples/
clips/
*.zip
pronunciations.csv

Troubleshooting

Weird layout? Use voila TTSNotebook1.ipynb instead of running in Jupyter.

PDF text missing? It might be scanned—OCR first, then paste text.

Databricks (brief)

Repos → add this repo.

%pip install -r /Workspace/Repos/<you>/TTS/requirements.txt

Prefer hosting Voilá externally; call Databricks via REST/SQL endpoints from the app.

License

See LICENSE.
