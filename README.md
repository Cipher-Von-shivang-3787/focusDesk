# FocusDesk

Built for my friend Dev during the DEV Hacktoberfest Weekend Challenge: Build for a Friend (October 2026).
All code was written during the challenge window.

FocusDesk is a study planner, Pomodoro timer and **notes-to-quiz** tool. A small open-weight model runs **locally with Ollama** and writes quizzes from your own notes. Your notes never leave your computer, and it works offline once the model is downloaded.

## Features
- **Pomodoro timer:** focus, short break and long break, with adjustable lengths.
- **Study tasks:** estimated pomodoros per task, an active task, and daily stats (sessions, focus minutes, day streak).
- **Notes to quiz:** paste notes, get multiple-choice questions with explanations.
- **Spaced repetition:** missed questions come back after 0, 1, 3, 7, 14 and 30 days.
- **Weak-spot memory:** the app tracks topics you miss and asks the model for more questions on them.
- **Backup and restore:** save everything to a file (Settings). Your API key is never included.

## Models
- **Recommended: `phi4-mini`** (Microsoft, MIT license). Fast on a normal laptop and returns clean JSON. This is the model I use for quizzes.
- **DeepSeek-R1** (`deepseek-r1:8b`, distilled, MIT license) also works, but it writes out its reasoning before answering, so a quiz can take a minute or more on a laptop. The app's initial model setting is `deepseek-r1:8b`, so change it in Settings if you want `phi4-mini`.
- Any other Ollama model works too. Type its name in **Settings > Model**.
- Optional: Claude (Anthropic API) can be selected as a provider by pasting an API key in Settings. The project is built around the local open model.

## Setup on Windows 11
1. Install Ollama from https://ollama.com/download.
2. Open PowerShell and download the model:
   ```
   ollama pull phi4-mini
   ```
3. Allow the web page to reach Ollama, then quit and reopen Ollama from the system tray:
   ```
   setx OLLAMA_ORIGINS "*"
   ```
4. Check `http://localhost:11434` in your browser. It should say "Ollama is running".
5. Open `index.html` (double-click it).
6. Go to **Settings**, set **Model** to `phi4-mini`, and click outside the box to save.
7. Go to **Quiz**, paste about a page of notes, and press **Make quiz from notes**.

If you prefer a local server (needed for the installable PWA features):
```
python -m http.server 8000
```
Then open `http://localhost:8000`.

## Troubleshooting
- **Could not reach Ollama:** make sure Ollama is running and you restarted it after `setx OLLAMA_ORIGINS`.
- **Model not found:** the name in Settings must match `ollama list` exactly.
- **Model did not return valid JSON:** try shorter notes (about a page) or press the button again.

## Files
`index.html` app, `sw.js` offline cache, `manifest.json` and icons for install, `LICENSE` (MIT).
