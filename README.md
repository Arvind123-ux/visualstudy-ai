# VisualStudy AI

Turn any textbook diagram into an interactive lesson. Upload a diagram, get an explanation, a quiz and revision notes, in English or Hindi. Runs on **open-weight Gemma 4**, locally or through the Gemini API.

![demo](demo.gif)

## What it does

- Upload a diagram (biology, networks, flowcharts, circuits)
- Gemma 4 vision explains each labelled part in simple language
- Hindi / English output, Beginner / Intermediate / Advanced levels
- Auto-generated 5-question quiz with explanations, plus revision notes
- **"AI is not sure" list**: the model flags labels it cannot read clearly, instead of guessing

## How Gemma 4 is used

Gemma 4 is the only model in the project. The image goes straight to its vision input, and it returns structured JSON (topic, components, quiz, notes, uncertain items) that the frontend renders.

Two backends, switched by one line in `backend/.env`:

| Mode | Setting | Why |
|---|---|---|
| Local (open weights) | `PROVIDER=ollama` | Works offline, image never leaves your laptop |
| Gemini API | `PROVIDER=gemini` | Larger Gemma 4 variants, faster on weak hardware |

## Run it

    git clone https://github.com/Vivan217/visualstudy-ai.git
    cd visualstudy-ai/backend
    python3 -m venv venv && source venv/bin/activate
    pip install flask flask-cors requests python-dotenv
    cp .env.example .env     # then edit it
    python app.py

Open `frontend/index.html` in a browser.

For local mode: install [Ollama](https://ollama.com), then `ollama pull gemma4:e2b` and set `PROVIDER=ollama`, `OLLAMA_MODEL=gemma4:e2b`.

## Local vs API (honest notes)

TODO: fill after testing (speed on MacBook Air, label accuracy, Hindi quality).

## Project layout

    backend/app.py        Flask API, calls Gemma 4
    frontend/index.html   single-file UI, no build step
    SKILL.md              lets coding agents call the API

## Contributing

PRs welcome (Hacktoberfest). Good first issues: click-to-learn on diagram regions, more subjects, tests, a nicer UI.

## License

MIT
