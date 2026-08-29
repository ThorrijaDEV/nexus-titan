# THORRIJA NEXUS TITAN

Personal Digital Intelligence, Infrastructure, Network, RF, Security, Automation and AI Operations Platform.

A modular, local-first, desktop-first intelligence and operations platform. Everything observable becomes data. Everything becomes an event. Everything can be correlated. AI can reason over the entire system.

## What is it?

A unified platform for personal infrastructure observability and AI-assisted operations. Nexus collects telemetry from the local system (processes, network, hardware, logs, RF spectrum, security events), stores it in a local time-series database, exposes it via a real-time API and WebSocket bus, and provides a React/TypeScript GUI for visualization and interaction. An AI agent can query, correlate, and reason over the entire dataset.

## What does it do?

- **Event bus**: Central nervous system — all collectors publish, all consumers subscribe
- **Collectors (modular)**: system metrics (psutil), network listeners (port-authority), process tree (process-ecosystem-monitor), Wi-Fi/BLE environment (wifi-time-machine, ble-radar), RF spectrum, log parsers, security events
- **Storage**: SQLite (local-first, WAL mode) with time-series tables; configurable retention
- **Real-time**: WebSocket broadcast to GUI; API for historical queries
- **Frontend**: React 18 + TypeScript + Vite, Zustand state, TanStack Query, Recharts
- **AI integration**: Backend exposes tools for LLM function calling (query metrics, correlate events, summarize anomalies, propose actions)
- **Local-first**: No cloud dependencies; everything runs on your machine; data never leaves

## Architecture

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ Collectors  │────▶│  Event Bus  │────▶│  Storage    │
│ (modular)   │     │  (in-memory)│     │  (SQLite)   │
└─────────────┘     └──────┬──────┘     └──────┬──────┘
                           │                   │
                    ┌──────▼──────┐     ┌──────▼──────┐
                    │   WebSocket │     │    API      │
                    │   Broadcast │     │  (FastAPI)  │
                    └──────┬──────┘     └──────┬──────┘
                           │                   │
                    ┌──────▼───────────────────▼──────┐
                    │       Frontend (React/TS)       │
                    │  Dashboard, Graphs, AI Chat     │
                    └─────────────────────────────────┘
```

| Layer | Technology |
|-------|------------|
| Backend | Python 3.13, FastAPI, uvicorn, aiosqlite, psutil, numpy |
| Storage | SQLite (local-first), time-series tables |
| Real-time | WebSocket event broadcast to GUI |
| Frontend | React 18, TypeScript, Vite, Zustand, TanStack Query, Recharts |

## Quick Start

```bash
# Backend
cd backend
uv venv
uv pip install -e .
uv run nexus --dev

# Frontend
cd frontend
npm install
npm run dev
```

Open http://localhost:5173 (frontend) or http://localhost:7860/docs (API).

## Status

**In Active Development**

Core architecture defined, event bus implemented, collector framework ready, backend/frontend scaffolding complete. Phase 1 collectors (system, network, process) in progress. Specification in `prompt.md`, phased plan in `docs/PHASES.md`.

## Repository Note

This repository contains documentation only. The implementation is private code.

## License

MIT