# 🎬 Momentify: AI-Powered Sports Highlight Generator

**Momentify** is your smart assistant for pulling out jaw-dropping moments from full-length sports matches. Whether you want to see just "Messi goals", "penalties", or "wild celebrations", Momentify delivers only the parts you care about — automatically.

---

## 💡 How It Works

1. Upload a `.mp4` sports match  
2. Enter a query like:  
   - `"Messi goals"`  
   - `"fouls and red cards"`  
   - `"celebrations"`
3. We:
   - 🔊 Transcribe the entire audio using Whisper (fast on GPU)
   - 🤖 Send the transcript + your query to **LLaMA 4** via **Groq**
   - 🧠 Extract highlight timestamps from the LLM's JSON output
   - ✂️ Use MoviePy to cut and stitch your final highlight reel
4. Download your custom-made highlights in seconds

---

## ⚙️ Tech Stack

| Component         | Purpose                                                              |
|------------------|----------------------------------------------------------------------|
| `Whisper`         | Transcribe speech to text                                            |
| `Groq + LLaMA 4`  | Understand your query & transcript to find key moments              |
| `MoviePy`         | Cut and merge video clips                                            |
| `Gradio`          | Slick UI to upload & interact with your highlight generator         |
| `Kaggle GPU (A100)` | Whisper runs much faster using a GPU (especially the A100)         |

---

## 🧱 Notebook Structure

1. **Install Dependencies**  
   Install Whisper, MoviePy, Groq SDK, and Gradio via `pip install`

2. **Imports & API Setup**  
   Import required libraries and securely load `GROQ_API_KEY` from Kaggle Secrets

3. **Transcription**  
   Whisper converts the audio in the video to text — GPU makes this blazing fast

4. **Highlight Extraction via Groq**  
   The transcript and user query are sent to **LLaMA 4** via Groq API  
   The prompt ensures the output is **strict JSON** like:

   ```
   {
     "segments": [
       { "start": 52, "end": 58 },
       { "start": 108, "end": 112 }
     ]
   }
   ```

   We also truncate the transcript input to stay within Groq's token limit

5. **Video Slicing**  
   Using MoviePy to subclip and combine segments based on those timestamps

6. **Gradio Interface**  
   Simple drag-and-drop UI with a textbox query for the type of highlights you want

---

## 🚀 How to Run It

> Recommended: Run on Kaggle with GPU (A100 or T4)

1. Enable GPU: `Settings > Accelerator > GPU (T4, V100, A100)`
2. Upload your `.mp4` video to `/kaggle/input/`
3. Run the notebook cells in order (already modularized)
4. The Gradio UI will launch — just upload and query!

---

## 🧠 Prompt Engineering Highlights

We designed the prompt to:
- Return only valid **parseable JSON**
- Skip all explanations, markdown, or code formatting
- Include extra context around timestamps (by ±5 seconds)
- Stay under Groq's token limit by truncating the transcript when needed

This gives us a **clean interface between LLM and video editing**, with minimal post-processing.

---

## 📌 Notes

- Momentify works best on **sports content** with clear commentary
- LLaMA 4 runs through **Groq** for low-latency, high-speed inference
- All API keys are managed safely using **Kaggle Secrets**
- MoviePy rendering may take time depending on video resolution & segment count

---

> Made with ❤️ by Hussain Alyafei 
> License: MIT

---
