
# AI Study Tutor

A conversational AI tutor built with Google's Gemini 2.5 Flash, designed to help students get clear, structured answers to study-related questions across any subject.

**Live demo:** https://huggingface.co/spaces/thabassum9/ai_tutor

## What it does

Ask it anything you'd normally ask a tutor — a concept you're stuck on, a numerical problem, a piece of code you don't understand — and it responds with:

- Clear, simple explanations broken into steps
- Worked examples where they help
- Full calculation steps for numerical problems
- Commented code when a programming question is asked, with line-by-line breakdowns on request
- Headings, bullet points, or tables when that makes the answer easier to scan

The tutor is built around a custom system prompt that enforces this structure on every response, rather than leaving formatting and depth up to chance.

## Tech stack

- **Gemini 2.5 Flash** (`google-genai` SDK) — the underlying model, accessed via chat sessions to maintain conversation context
- **Gradio** — chat UI, deployed as a `ChatInterface`
- **Hugging Face Spaces** — hosting

## How it works

Each session opens a persistent `chat` object via the Gemini API, so the model retains context across turns within a conversation. The system instruction is set once at session creation and shapes every response — it's what keeps answers consistently structured instead of freeform.

The API key is stored as a Hugging Face Space secret and read from the environment at runtime, not hardcoded.

## Running it locally

```bash
pip install gradio google-genai
```

Set your Gemini API key as an environment variable:

```bash
export GEMINI_API_KEY="your-key-here"
```

Then run:

```bash
python app.py
```

## Notes

This is a single-model wrapper, not a RAG system — it doesn't pull from external study material or a knowledge base. Its value is in the prompt engineering that shapes how Gemini responds to study questions, not in retrieval or fine-tuning.
