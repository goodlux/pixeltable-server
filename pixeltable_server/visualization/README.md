# Pixeltable Visualization Server

Browser-based visualization for Pixeltable with interactive pipeline explorer.

## Features

- Interactive table browser with React Flow visualizations
- Real-time WebSocket updates
- ProcessPoolExecutor for async/Pixeltable compatibility
- Auto npm install/build on first run

## Architecture

```
Browser ←─ WebSocket ─→ FastAPI (async) ─→ ProcessPoolExecutor ─→ Pixeltable (worker processes)
```

The FastAPI server stays async while Pixeltable operations run in isolated worker processes to avoid threading conflicts.

## Running

```bash
# From pixeltable-server root
python -m uvicorn pixeltable_server.visualization.api.main:app --host 0.0.0.0 --port 7777
```

Then open http://localhost:7777 in your browser.

## Development

**UI Development:**
```bash
cd pixeltable_server/visualization/ui
npm install
npm run dev  # Vite dev server on port 5173
```

**Production Build:**
```bash
cd pixeltable_server/visualization/ui
npm run build  # Creates dist/ folder
```

## Files

- `api/main.py` - FastAPI server with WebSocket endpoints
- `executor.py` - ProcessPoolExecutor manager
- `worker.py` - Worker functions that run Pixeltable in isolated processes
- `ui/` - React + TypeScript + Tailwind + React Flow frontend

## Note

This was originally prototyped in the MCP (mcp-server-pixeltable-developer) and moved here for production development.
