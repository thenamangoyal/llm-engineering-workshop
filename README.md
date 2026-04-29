# Agentic LLMs in Practice — Workshop Notebook

> A hands-on Colab notebook accompanying the workshop *"Agentic LLMs in Practice — Tools, Function Calling, and Workflow Design"*, ODSC AI East 2026, April 30, 2026.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/thenamangoyal/llm-engineering-workshop/blob/main/Agentic_LLMs_Workshop.ipynb)

## What's in the notebook

By the end of this notebook you will have built — with no API keys required —

1. **Module 1 — Function calling, end to end.** A function-calling agent loop on SQLite + a mock weather API, with strict Pydantic-validated tool arguments.
2. **Module 2 — Reference architectures.** A router-worker state machine with Pydantic contracts at every node, compared head-to-head with a free-form ReAct loop.
3. **Module 3 — Surviving production.** A retry-storm demo on a deliberately flaky upstream, with a *playground cell* where you tune the retry policy yourself and watch the bars move.
4. **Module 4 — Observability.** An OpenTelemetry-style traced agent run, rendered as a Gantt chart you generate from your own spans.

Each module produces a real, inline visual you can copy into your own slides.

## How to run

The notebook is designed to run with **no setup beyond pip install**, on two environments:

### 🚀 Path A — Free Google Colab (recommended)

1. Click the **Open in Colab** badge above.
2. `Runtime → Change runtime type → T4 GPU`.
3. `Runtime → Run all` (`⌘/Ctrl + F9`). Whole notebook completes in **~5 minutes**.

The default model is **Qwen/Qwen3.5-4B** (~8 GB at fp16, fits Colab T4 easily). Native tool calling. No API keys.

### 💻 Path B — Local MacBook (Apple Silicon recommended)

```bash
# one-time install:
pip install -r requirements.txt
jupyter lab Agentic_LLMs_Workshop.ipynb
```

The notebook auto-detects MPS (Apple Silicon GPU) and runs in fp16. Whole notebook completes in **~10–15 minutes** on an M-series Mac. CPU fallback works too.

### (Optional) Gemini Pro Preview comparison

If you have a Google AI Studio API key, add it to Colab Secrets as `GEMINI_API_KEY`. The notebook will then use Gemini 3.x Pro Preview alongside Qwen for one comparison cell. Off by default — the notebook works fully without it.

## What you'll see

| Module | Visual you produce |
|---|---|
| 1 | A 3-panel chart: questions answered, latency per question, total tokens. |
| 2 | Side-by-side bars: % right tool / latency / steps for the two architectures. |
| 3 | Side-by-side bars + a *playground* where you tweak retry params and the bars update. |
| 4 | A Gantt chart of the agent's parent-child span tree. |

## Author

**Naman Goyal**, Machine Learning Engineer at Google DeepMind.
Personal views; synthesis of publicly available engineering practice. Not affiliated with or representative of Google DeepMind.

## References (all public docs)

- LangGraph — https://langchain-ai.github.io/langgraph/
- Plan-and-Execute pattern (LangChain blog) — https://blog.langchain.dev/planning-agents/
- Tenacity — https://tenacity.readthedocs.io/
- Function-calling guide (OpenAI) — https://platform.openai.com/docs/guides/function-calling
- ReAct (Yao et al., 2022) — https://arxiv.org/abs/2210.03629
- OpenTelemetry — https://opentelemetry.io/

## License

[MIT](LICENSE) — take what's useful.
