---
name: visualstudy-diagram-explainer
description: Explain an educational diagram image, generate a quiz and revision notes using Gemma 4 through the local VisualStudy AI backend. Use when the user shares a textbook diagram, flowchart or scientific illustration and wants to understand or revise it.
---

# VisualStudy diagram explainer

Requires the backend running at http://127.0.0.1:5000 (see README).

## Steps

1. Ask which language (English or Hindi) and level (Beginner, Intermediate, Advanced) if the user did not say.
2. Send the image:

        curl -s -F image=@PATH_TO_IMAGE -F lang=English -F level=Beginner http://127.0.0.1:5000/api/analyze

3. The reply is JSON with: topic, summary, components, quiz, notes, uncertain.
4. Present the topic and components first, then offer the quiz one question at a time.
5. Always show the "uncertain" items to the user. Do not present them as facts.

## Notes

- If the reply contains "error", show it and suggest checking backend/.env.
- Treat explanations as study help, not as a replacement for the textbook.
