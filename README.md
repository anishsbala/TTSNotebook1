# Text-to-Speech Studio (Jupyter)

Jupyter/ipywidgets app to turn text or PDFs into speech using OpenAI TTS,
with speaker detection and a pronunciation dictionary.

## Quick start
```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
source .venv/bin/activate
pip install -U pip -r requirements.txt
cp api.env.example api.env   # put your OPENAI_API_KEY in here
mkdir -p clips samples
jupyter lab  # or: jupyter notebook
