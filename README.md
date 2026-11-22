# Yumi — Self-Hosted Multi-Tool AI Agent & RAG Stack

Production-ready, privacy-first AI assistant architecture built with **n8n**, **Qdrant Vector Database**, **Google Gemini LLM**, and **Caddy Reverse Proxy** inside **Docker**.

## Architecture & Key Features
- **Autonomous AI Agent (Tool Calling):** Dynamically routes user requests between conversational memory, external REST APIs (real-time weather via Open-Meteo), and internal knowledge base search.
- **Persistent RAG Pipeline:** Document ingestion workflow via web form (`Binary` loader + `Gemini Embeddings`) stored persistently on disk using **Qdrant** (`qdrant_data` volume).
- **Conversational Memory:** Context-aware multi-turn dialogue isolated per Telegram `chat.id`.
- **Production Security:** Isolated Docker internal network (`http://qdrant:6333`), automatic HTTPS/SSL termination via **Caddy**, and UFW firewall hardening.

## Quick Start (Production)
1. Update domain name in `Caddyfile` and `docker-compose.prod.yml`.
2. Validate configuration:
   ```bash
   docker compose -f docker-compose.prod.yml config --quiet
   ```
3. Launch stack:
   ```bash
   docker compose -f docker-compose.prod.yml up -d
   ```
4. Import `yumi-agent-workflow.json` into n8n and configure credentials (Telegram Bot Token & Gemini API Key).
