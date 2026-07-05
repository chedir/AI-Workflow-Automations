AI Workflow Automations

A small toolkit of AI-assisted research workflows for tracking technology and market trends from video and macro data. Scripts and prompts specified by me, implemented with AI coding tools.

Intentionally semi-manual, not a hands-off pipeline — see "Approach."

Components


transcript-capture/ — Fetches a video transcript, date-stamped. Run per-video.
trend-analysis/ — Prompt for an AI agent to review a folder of grouped transcripts and return a summary and what changed.
macro-data/ — Pulls and tracks a defined set of macro/market indicators.
agent-procedures/ — Operating procedures for AI monitoring tasks (verification rules, thresholds, status logic). Generalized.


Weekly flow

Capture transcripts per video → group by source into a folder → point the agent at the folder for a trend read → run the macro script. Loosely coupled, run in sequence.

Approach


Semi-manual by design. Bulk transcript pulls got rate-limited as bot traffic, so per-video is more reliable — and curating what to analyze beats full automation, which produces mostly noise.
Mixed models. Local open-source (Ollama) for light work like transcription; frontier models for reasoning and summarization. Splitting by task keeps token cost sustainable.


Notes


API keys and personal data removed; placeholder credentials used.
Personal research, shared as-is.
