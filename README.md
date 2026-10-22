# volxa-ai-voice-sales-agent.
Volxa is an AI-powered voice sales agent that enables real-time, multilingual conversations with customers. It answers product-related questions, explains features, handles customer objections, and helps convert potential customers into buyers.
# Voxa — AI Voice Sales Agent

A Flask + SQLite starter project for live AI sales calls. It includes a sales call screen, live transcript, browser speech recognition and speech playback, call timer/status, consent gate, audio recording storage, AI-generated call summary, sales status, and call history.

## Features mapped to the project brief
- **Voice conversation:** browser speech recognition transcribes customer speech; Gemini generates natural sales responses; browser speech synthesis speaks replies.
- **Languages:** English, Hindi, Marathi, Gujarati, Bengali, Tamil, Telugu, Kannada, Malayalam and Spanish. Actual speech recognition/voices depend on browser and OS support.
- **Live transcript:** customer and AI turns appear on the Sales Calls page.
- **Call controls:** Start Call, End Call, elapsed timer, live/ended status.
- **Recording consent:** requires a confirmation checkbox and confirmation dialog before a call can start; saved recordings are stored in SQLite and playable in Call History.
- **AI summary:** after ending a call, the backend asks Gemini for summary, customer requirements, objections and next steps.
- **Sales status:** Gemini assigns one of Converted, Interested, Follow-up Required, Not Interested, Demo Requested, No Response.
- **Call history:** prior calls show transcript, summary, requirements, objections, next steps, status, duration and associated recording when available.

## Important audio limitation
The included browser `MediaRecorder` captures the microphone/customer side. Browser `speechSynthesis` output is not mixed into that recording, so this starter does **not yet produce a single mixed recording of both customer and AI audio**. To satisfy full-call recording, integrate an audio pipeline that records both tracks (for example, provider-generated TTS audio plus the microphone track and server-side mixing, or an approved tab-audio capture workflow). Do not claim a complete mixed call recording until that is implemented and tested.

## Setup (Windows / VS Code)
1. Extract the ZIP and open the `voice-ai-chatbot` folder in VS Code.
2. In the terminal, run:
   ```powershell
   python -m venv .venv
   python -m pip install -r requirements.txt
   ```
3. Copy `.env.example` to `.env` and add a valid Gemini API key from https://aistudio.google.com/app/apikey:
   ```dotenv
   GEMINI_API_KEY=your_actual_api_key_here
   GEMINI_MODEL=gemini-2.5-flash
   PORT=5000
   ```
4. Start the app:
   ```powershell
   python app.py
   ```
5. Open http://127.0.0.1:5000 in Chrome or Edge.
6. Open **Sales Calls**, confirm recording consent, and click **Start Call**. Speak through the microphone, or use the text box to test without speech recognition. Click **End Call** to generate a summary and status.

## Database
`chatbot.db` is created automatically. It stores general chat messages, settings, sales calls, call transcript messages, and audio recordings as SQLite BLOBs. Call history is available from the sidebar.
