# 🎬 Momentify: AI-Powered Sports Highlight Generator

**Momentify** is your smart assistant for pulling out jaw-dropping moments from full-length sports matches. Whether you want to see just "Messi goals", "penalties", or "wild celebrations", Momentify delivers only the parts you care about — automatically.

---

## 💡 How It Works (TL;DR)

1. Upload a `.mp4` sports match
2. Enter a query like:  
   `"Messi goals"` or `"fouls and red cards"` or `"celebrations"`
3. We:
   - 🔊 Transcribe the entire audio using Whisper (fast on GPU)
   - 🤖 Send the transcript + your query to **LLaMA 4** via **Groq**
   - 🧠 Extract highlight timestamps from the LLM's JSON output
   - ✂️ Use MoviePy to cut and stitch your final highlight reel
4. Download your custom-made highlights in seconds

---

## ⚙️ Tech Stack

| Component | Purpose |
|----------|---------|
| `Whisper` | Transcribe speech to text |
| `Groq + LLaMA 4` | Understand your query & transcript to find key moments |
| `MoviePy` | Cut and merge video clips |
| `Gradio` | Slick UI to upload & interact |
| `Kaggle GPU (A100)` | High-performance processing (Whisper on GPU = much faster!) |

---

## 🧱 Notebook Structure

1. **Install Dependencies**  
   `pip install` everything you need (Whisper, MoviePy, Groq, Gradio)

2. **Imports & API Setup**  
   Load `GROQ_API_KEY` securely via Kaggle Secrets

3. **Transcription**  
   Run Whisper on GPU to speed things up significantly (A100 is 🔥)

4. **Highlight Extraction via Groq**  
   The prompt is crafted with care — instructing LLaMA 4 to return only **valid JSON** in a format like:
   ```json
   {
     "segments": [
       { "start": 52, "end": 58 },
       { "start": 108, "end": 112 }
     ]
   }
