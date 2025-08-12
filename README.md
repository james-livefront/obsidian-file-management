# Obsidian File Management Templates

A collection of Templater scripts for batch file management in Obsidian.

## Features

### 1. Batch Rename and Title (`batch-rename-titles.md`)
- Renames files that are all numbers (Zettelkasten IDs) or start with "Untitled"
- Adds or updates titles based on file content
- Handles "Untitled" titles in existing files
- Works recursively through all vault folders
- Preview mode to see changes before applying

### 2. Delete Empty Files (`delete-empty-files.md`)
- Finds and removes empty or near-empty files
- Multiple detection modes (all files vs. Untitled only)
- Aggressive content detection (removes metadata, formatting, etc.)
- Size analysis tools
- Moves files to trash (recoverable)

## Installation

1. Copy the template files to your Obsidian Templater templates folder (usually `Templates/`)
2. Ensure Templater plugin is installed and configured
3. Set up your Templater folder in settings if not already done

## Usage

### For Batch Rename:
1. Open command palette (Cmd/Ctrl + P)
2. Run "Templater: Insert template"
3. Select `batch-rename-titles`
4. Choose your processing mode:
   - Preview only (recommended first)
   - Process all files
   - Select specific folder
   - Process only Zettelkasten files
   - Process only Untitled files

### For Empty File Deletion:
1. Open command palette (Cmd/Ctrl + P)
2. Run "Templater: Insert template"
3. Select `delete-empty-files`
4. Choose your action:
   - Preview ALL empty files
   - Preview only Untitled empty files
   - Analyze file sizes
   - Show smallest files first

## License

MIT
