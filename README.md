# FocusDesk

Study planner + Pomodoro timer + **notes-to-quiz** powered by **DeepSeek-R1** (open weights, MIT license) running locally with Ollama. Claude (Anthropic API) is an optional extra provider. Installable as a PWA. No backend, no API keys, no accounts.

## Choose your AI
Open **Settings**. The default is DeepSeek via Ollama, which keeps everything on your machine. You can switch to Claude by pasting an API key (stored only in your browser).

## Run it
```
ollama pull deepseek-r1:8b
OLLAMA_ORIGINS="*" ollama serve
python3 -m http.server 8000   # then open http://localhost:8000
```

## How the quiz works
1. Paste notes (or load a .txt/.md file) and press **Make quiz**.
2. The local model writes multiple-choice questions as JSON.
3. Every card goes into a spaced-repetition deck (Leitner boxes: 0, 1, 3, 7, 14, 30 days). Missed cards drop back to box 0.
4. **Review due cards** replays whatever is due today.

## Using it on a phone
Host the folder on GitHub Pages and install it from the browser menu. The timer, tasks and review deck work offline. Generating new quizzes needs Ollama, so make them on the laptop, press **Export deck**, and **Import deck** on the phone.

## Files
`index.html` app · `sw.js` offline cache · `manifest.json` + icons for install

## Memory
- Tasks, stats, the quiz deck and settings are saved in the browser. Use **Settings > Back up everything** to save them to a file and **Restore from backup** to load them again (the API key is never included).
- The app tracks which topics you miss. Your weakest topics are sent with each new quiz request so the model asks more about them.
