# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Aztec Log Viewer is a single-file HTML application for visualizing Aztec E2E test logs. It parses structured log output and provides three viewing modes for analysis.

## Running the Application

Open `log-viewer.html` directly in a browser. No build step, dependencies, or server required.

## Architecture

The entire application is contained in `log-viewer.html`:
- **CSS** (lines 7-1180): Dark theme styling with CSS variables for colors
- **HTML** (lines 1180-1485): Three view containers (Logs, Time Travel, System Map)
- **JavaScript** (lines 1486-end): Application state and logic

### Log Format

The parser expects logs matching this regex:
```
/^(\d{2}:\d{2}:\d{2})\s+\[(\d{2}:\d{2}:\d{2}\.\d{3})\]\s+(INFO|VERBOSE|WARN|ERROR|DEBUG):\s+(\S+)\s+(.*)$/
```
Example: `14:32:01 [00:01:23.456] INFO: aztec:pxe Message text`

### Three Viewing Modes

1. **Logs Mode**: Traditional log viewer with filtering by level (error/warn/info/verbose/debug), module tree sidebar, and text search with highlighting

2. **Time Travel Mode**: Playback logs chronologically with variable speed (0.25x-100x), timeline scrubber, module activity lanes showing when each module was active

3. **System Map Mode**: Canvas-based visualization showing module relationships, interaction flows between modules, with configurable layout (grid/hierarchy) and grouping depth

### Key State Variables

- `logEntries[]`: Parsed log entries with timestamp, level, module, message, and optional JSON data
- `modules`: Map of module names to log counts
- `activeModules`/`activeLevels`: Current filters
- `ttCurrentTimeMs`/`ttPlaying`: Time travel playback state
- `smCurrentTimeMs`/`smPlaying`: System map playback state
- `smModuleInteractions`: Map tracking which modules interact within time windows

### Input Methods

- Paste log text directly into textarea
- Drag and drop log files
- File picker button

The app also parses optional metadata headers (Parent Log, Command, Commit, Env, Date, System, Resources, History) and test results (PASS/FAIL lines).
