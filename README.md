# Aztec Log Viewer

A browser-based log viewer for analyzing Aztec E2E test logs. No installation required - just open the HTML file in your browser.

## Usage

1. Open `log-viewer.html` in a browser
2. Paste log content into the text area, or drag and drop a log file
3. Click "Parse Logs" to analyze

## Features

### Logs Mode

Traditional log viewer with powerful filtering:

- **Level filtering**: Toggle visibility of ERROR, WARN, INFO, VERBOSE, and DEBUG messages
- **Module tree**: Hierarchical view of all logging modules with message counts
- **Text search**: Filter logs by keyword with match highlighting
- **JSON expansion**: Inline expand/collapse for log entries containing JSON data
- **Auto-scroll**: Optional auto-scroll to follow new entries

### Time Travel Mode

Replay logs chronologically to understand event sequences:

- **Playback controls**: Play, pause, step forward/back, skip to start/end
- **Variable speed**: 0.25x to 100x playback speed
- **Timeline scrubber**: Click or drag to jump to any point in time
- **Activity lanes**: Visual timeline showing when each module was active
- **Error/warning markers**: Timeline markers highlight problematic moments

### System Map Mode

Visualize module interactions and system architecture:

- **Module nodes**: Boxes sized by log volume, colored by activity state
- **Interaction flows**: Lines connecting modules that log within the same time window
- **Layout options**: Grid or hierarchical arrangement
- **Grouping depth**: Control how module namespaces are collapsed
- **Playback**: Animate the system map over time to see interaction patterns

## Log Format

The viewer parses logs in this format:

```
HH:MM:SS [HH:MM:SS.mmm] LEVEL: module:name Message text
```

Example:
```
14:32:01 [00:01:23.456] INFO: aztec:pxe Starting PXE service
14:32:01 [00:01:23.789] DEBUG: aztec:pxe:sync Syncing blocks {"fromBlock": 0, "toBlock": 100}
```

### Metadata Headers

The viewer recognizes optional metadata at the start of log files:

- `Parent Log:` - Link to parent log
- `Command:` - Command that generated the logs
- `Commit:` - Git commit hash
- `Env:` - Environment information
- `Date:` - Timestamp
- `System:` - System information
- `Resources:` - Resource allocation

### Test Results

Lines starting with `PASS` or `FAIL` are parsed and displayed in a summary section.

## License

MIT
