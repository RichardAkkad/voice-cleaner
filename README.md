### Voice Note Cleaner

Upload a messy voice note and get a clean transcript. Everything runs locally, so no audio leaves your computer.

#### How it works
1. You upload an audio file (m4a, mp3, wav) in the web page.
2. The FastAPI backend transcribes it with **faster-whisper**.
3. The transcript is sent to a local LLM (**Qwen 2.5 7B** via **Ollama**), which removes filler words, false starts and repetitions without changing the meaning.
4. The page shows the raw transcript and the cleaned version side by side.

#### Tech stack
Python, FastAPI, faster-whisper, Ollama, Qwen 2.5, HTML/JavaScript

#### Requirements
- Python 3.10 to 3.12 (3.15 is too new for some dependencies)
- [Ollama](https://ollama.com) with the model pulled: `ollama pull qwen2.5:7b`

#### Run it
```bash
pip install -r requirements.txt
uvicorn app:app --reload
```
Open http://127.0.0.1:8000 and upload a recording. The first run downloads the Whisper `small` model (about 500 MB).

#### Notes
- Whisper drops many "um"s on its own. An `initial_prompt` containing fillers is used to keep more of them in the raw transcript.
- Long recordings can take a few minutes on CPU.

  below is example of a cleaned up messy voice note
<img width="1059" height="772" alt="Screenshot 2026-10-11 132434" src="https://github.com/user-attachments/assets/de280131-3a1b-4a9d-a476-5db52d7655a1" />
