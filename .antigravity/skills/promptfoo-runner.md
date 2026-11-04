---
name: promptfoo-runner
description: "Interactive skill for running, inspecting, and debugging promptfoo evaluations across Levels 0 through 8 (including LM Studio and Ollama) in Antigravity."
---

# Promptfoo Runner Skill for Antigravity

This skill provides direct terminal recipes, debugging strategies, and workflow automation for running LLM evaluations in this repository.

## Quick CLI Execution Commands

Run these commands directly in the Antigravity terminal or via the agent `run_command` tool:

### 1. Progressive Suite Execution (By Level)

```bash
# Run Level 0: Minimal Smoke Test
npm run eval:0

# Run Level 1: Deterministic Basics (equals, contains, regex, is-json)
npm run eval:1

# Run Level 2: Chain-of-Thought & Chat Inspection (<thinking> tags & reasoning)
npm run eval:2

# Run Level 3: LLM-as-a-Judge Rubrics (tone, empathy, refusal safety, pedagogy)
npm run eval:3

# Run Level 4: Model vs Model Benchmarking (Side-by-side head-to-head)
npm run eval:4

# Run Level 5: Performance Gating (latency SLA, cost bounds, rubric thresholds)
npm run eval:5

# Run Level 7: Local Model Evaluation via LM Studio (Gemma 3 1B / Nemotron)
npm run eval:7

# Run Level 7 without cache (force fresh generation from local model)
npm run eval:lmstudio

# Run Level 8: Local Reasoning & Thinking Trace Inspection (LM Studio)
npm run eval:8

# Run the complete test suite across all levels
npm run eval:all
```

### 2. Interactive Web UI & Reports

```bash
# Start promptfoo web viewer on port 15500
npm run view

# Export standalone HTML evaluation report
npm run export
```

---

## Targeted Debugging & Single-Test Execution

When investigating a test failure, avoid running the entire suite. Target the specific test or file:

```bash
# Run only a specific test file
npx promptfoo eval --tests tests/01_simple_assertions.yaml

# Run tests matching a specific description pattern
npx promptfoo eval --filter-description "Sally has 3 brothers"

# Run tests with verbose output to inspect raw model payloads
npx promptfoo eval --verbose

# Run without cache to bypass stored responses
npx promptfoo eval --no-cache
```

---

## Provider Troubleshooting & Key Configuration

- **Missing API Key**: Ensure `./.env` exists and contains `GEMINI_API_KEY` and/or `GOOGLE_API_KEY`. Promptfoo will automatically detect either variable.
- **Rate Limits (429)**: Promptfoo includes automatic retries (`retry: 2` in `./promptfooconfig.yaml`). For high concurrency, add `maxConcurrency: 2` to `defaultTest.options`.
- **Switching Models**:
  To benchmark against Groq or OpenRouter, export the respective key (`GROQ_API_KEY` / `OPENROUTER_API_KEY`) and uncomment the provider in `./promptfooconfig.yaml`.
- **Inspecting JSON Results**:
  Detailed test logs, raw prompt inputs, token counts, latency, and rubric reasoning are saved to `./output/eval-results.json`.

---

## Guidelines & Path Privacy

### Path Privacy & Hygiene Rule
Never print, reference, or leak local machine paths (e.g., `file:///Users/...`, `/Users/user/code/`, or home directory paths) in responses, code templates, logs, or comments. Always use relative workspace paths (e.g., `./tests/01_simple_assertions.yaml`, `./package.json`) or environment variable placeholders (e.g., `$WORKSPACE_ROOT`).
