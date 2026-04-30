# Agentic LLMs in Practice — Workshop Notebook

> A hands-on Colab notebook accompanying the workshop *"Agentic LLMs in Practice — Tools, Function Calling, and Workflow Design"*, ODSC AI East 2026, April 30, 2026.

**Pick the notebook that matches your machine:**

| Notebook | Where to run | One-click |
|---|---|---|
| `Agentic_LLMs_Workshop.ipynb` | Free Colab T4 GPU (or any Linux + CUDA) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/thenamangoyal/llm-engineering-workshop/blob/main/Agentic_LLMs_Workshop.ipynb) |
| `Agentic_LLMs_Workshop_Mac.ipynb` | Apple-Silicon Mac (M1/M2/M3/M4), via JupyterLab or VS Code | [Open in Colab](https://colab.research.google.com/github/thenamangoyal/llm-engineering-workshop/blob/main/Agentic_LLMs_Workshop_Mac.ipynb) (just for viewing — runs locally) |

Both notebooks have **identical content**: same modules, same exercises, same playground. Only the model backend differs (HF transformers + Qwen3.5-4B fp16 on Colab vs `mlx-lm` + Qwen3.5-4B-MLX-4bit on Mac).

## What's in the notebook

By the end of this notebook you will have built — with no API keys required —

1. **Module 1 — Function calling, end to end.** A function-calling agent loop on SQLite + a mock weather API, with strict Pydantic-validated tool arguments.
2. **Module 2 — Reference architectures.** A router-worker state machine with Pydantic contracts at every node, compared head-to-head with a free-form ReAct loop.
3. **Module 3 — Surviving production.** A retry-storm demo on a deliberately flaky upstream, with a *playground cell* where you tune the retry policy yourself and watch the bars move.
4. **Module 4 — Observability.** An OpenTelemetry-style traced agent run, rendered as a Gantt chart you generate from your own spans.

Each module produces a real, inline visual you can copy into your own slides.

## How to run

The notebook is designed to run with **no setup beyond pip install**, on two environments:

### 🚀 Path A — Free Google Colab (recommended for non-Mac users)

1. Click the Colab badge for `Agentic_LLMs_Workshop.ipynb` above.
2. `Runtime → Change runtime type → T4 GPU`.
3. `Runtime → Run all` (`⌘/Ctrl + F9`). The first cell installs `transformers` from HuggingFace `main` branch (~60 s) since Qwen 3.5 is a multimodal model that requires the latest class registration. Whole notebook completes in **~5 minutes** after that.

Model: **`Qwen/Qwen3.5-4B`** (~8 GB at fp16, fits Colab T4). Native tool calling via the chat template. No API keys.

### 💻 Path B — Apple-Silicon Mac with MLX (recommended for Mac users)

```bash
git clone https://github.com/thenamangoyal/llm-engineering-workshop.git
cd llm-engineering-workshop
pip install "mlx-lm>=0.31" "pydantic>=2.0" "tenacity>=9.0" matplotlib jupyter
jupyter lab Agentic_LLMs_Workshop_Mac.ipynb
```

Or open `Agentic_LLMs_Workshop_Mac.ipynb` in VS Code and Run All.

Model: **`mlx-community/Qwen3.5-4B-MLX-4bit`** (~2 GB on disk, 4-bit quantised). First load downloads weights into your HuggingFace cache (~30 s on a fast connection); subsequent loads are instant. Whole notebook completes in **~6–8 minutes** on an M-series Mac. No API keys.

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
