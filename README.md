
My Voice TTS (pt-BR)
===============================================================

Short description
-----------------
This repository holds the Phase 1 work to create a Text-to-Speech (TTS) model fine-tuned to the user's voice in Brazilian Portuguese (pt-BR), using Coqui TTS. The goal for this phase is a reproducible, Docker-based development environment that produces a fine-tuned model which can later be exported and optimized for offline use on a Samsung Galaxy S24.

Key choices
-----------
- Language: Brazilian Portuguese (pt-BR)
- Base framework: Coqui TTS (use a compatible pretrained model)
- Python: 3.11.9 
- Dev environment: Docker (recommended) or venv

Quickstart (Docker)
1. Build the development image (runs Jupyter by default):

```powershell
docker build -t my-voice-tts:latest .
```

2. Run a container (mount the project so work is persistent):

```powershell
docker run -it --rm -p 8888:8888 -v %cd%:/app my-voice-tts:latest
```

3. Open the notebook link printed by Jupyter in the container (http://localhost:8888).

If you prefer a native virtualenv instead of Docker (dev laptop):

```powershell
# using pyenv and venv on Windows (cmd.exe / PowerShell)
pyenv install 3.11.9
pyenv local 3.11.9
python -m venv .venv
.\.venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

Quickstart (Docker)
-------------------
1. Build the development image (runs Jupyter by default). If your Dockerfile is in docker/, specify it with -f:

```powershell
# PowerShell or CMD (from repo root)
docker build -f docker/Dockerfile -t my-voice-tts:latest .
```

2. Run a container (mount the project so work is persistent):

**PowerShell:**
```powershell
# Quick run
docker run -it --rm -p 8888:8888 -v "${PWD}:/app" my-voice-tts:latest

# Recommended: also mount data and models
docker run -it --rm -p 8888:8888 `
	-v "${PWD}:/app" `
	-v "${PWD}/data:/app/data" `
	-v "${PWD}/models:/app/models" `
	my-voice-tts:latest
```

**CMD (cmd.exe):**
```bat
:: Quick run
docker run -it --rm -p 8888:8888 -v %cd%:/app my-voice-tts:latest

:: Recommended: also mount data and models
docker run -it --rm -p 8888:8888 ^
	-v %cd%:/app ^
	-v %cd%/data:/app/data ^
	-v %cd%/models:/app/models ^
	my-voice-tts:latest
```

3. Open the notebook link printed by Jupyter in the container (http://localhost:8888).

If you prefer a native virtualenv instead of Docker (dev laptop):

```powershell
# using pyenv and venv on Windows (cmd.exe / PowerShell)
pyenv install 3.11.9
pyenv local 3.11.9
python -m venv .venv
.\.venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

Planned Repository layout
-----------------
- data/                  - training data, outputs... data 😬
- notebooks/             - Jupyter notebooks for each stage (audit, processing, training, export)
- models/                - downloaded base models, checkpoints, exports
- scripts/               - helper scripts (segmentation, normalization, export)
- docker/                - Docker files for reproducible dev environment
- requirements.txt       - pinned Python dependencies for venv or Docker
- README.md              

Success criteria for Phase 1
----------------------------
- A fine-tuned Coqui TTS model that produces intelligible pt-BR speech resembling my voice.
- Notebooks that reproduce data processing, training, and inference steps end-to-end inside Docker.
- An exported model (ONNX or other).

Next steps
-------------------------
1. Create a small runtime wrapper for Android (ONNX Runtime + JNI or use a microservice approach);
2. Build a Flutter plugin or FFI wrapper to consume the local runtime;
3. Build a simple Flutter app.
