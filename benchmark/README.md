# SciVisAgentBench MCP Logger

This directory contains the MCP (Model Context Protocol) logger for SciVisAgentBench evaluation.

## Files

- `mcp_logger.py` - Enhanced MCP communication logger with structured JSON logging and automatic screenshot capture
- `.gitignore` - Excludes log files and test data from version control

## Features

### Session-Based Logging
- Each logging session creates a unique timestamped directory under `communication_logs/`
- Directory structure: `communication_logs/session_YYYYMMDD_HHMMSS_mmm/`
- Contains JSON log file and screenshots subfolder

### Screenshot Management
The logger distinguishes between two types of screenshots:

1. **Auto-screenshots** (triggered after tool calls):
   - Not logged as communication events
   - Saved as PNG files with `"type": "auto_screenshot"`
   - Generated automatically after successful tool calls

2. **Agent-requested screenshots** (explicit get_screenshot calls):
   - Logged as communication events in JSON
   - Base64 image data replaced with placeholder in logs
   - Saved as PNG files with `"type": "agent_screenshot"`

### Communication Logging
- Records all MCP protocol communications with timestamps and sequence numbers
- Parses JSON messages and tracks tool calls
- Thread-safe logging with comprehensive error handling
- Session statistics and metadata

## Usage

```
"ParaView": {
    "command": "path to python in paraview_mcp conda env",
    "args": [
    "/paraview_mcp/benchmark/mcp_logger.py",
    "path to python in paraview_mcp conda env",
    "/paraview_mcp/paraview_mcp_server.py"
    ]
}
```

## Output Structure

```
communication_logs/
├── session_20250627_134610_050/
│   ├── mcp_communication.json      # Structured communication log
│   └── screenshots/
│       ├── screenshot_*.png        # Auto and agent screenshots
│       └── ...
└── session_20250627_140001_456/
    └── ...
```

## Log Format

The JSON log contains:
- Session metadata and statistics
- Sequential communication events with timestamps
- Parsed MCP messages and tool calls
- Screenshot tracking and metadata
- Error logging and debugging information
