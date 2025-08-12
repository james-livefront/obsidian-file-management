# Obsidian File Management Templates

A collection of Templater scripts for batch file management in Obsidian - clean up messy vaults with automated renaming, title management, and empty file detection.

## 🎯 Problem This Solves

Over time, Obsidian vaults accumulate:
- Files with numeric IDs (Zettelkasten) that need descriptive names
- "Untitled" notes from quick captures
- Empty or near-empty files cluttering your workspace
- Files without proper H1 titles
- Inconsistent naming conventions

These scripts automate the cleanup process while maintaining safety through preview modes and backups.

## ✨ Key Features

### Safety First
- **Preview Mode** - See exactly what will change before applying
- **Backup Lists** - Automatic file list creation before processing
- **Trash, Not Delete** - Files moved to `.trash` folder (recoverable)
- **Detailed Reports** - Timestamped reports for every operation
- **Folder Protection** - Automatically skips Templates, .trash, and .obsidian

### Smart Processing
- **Recursive** - Processes entire vault or specific folders with all subfolders
- **Batch Operations** - Handles thousands of files efficiently
- **Mode Selection** - Target specific file types or process everything
- **Error Handling** - Continues processing even if individual files fail
- **Progress Updates** - Real-time notifications during processing

## 📋 Business Rules

### Batch Rename Rules (`batch-rename-titles.md`)

The script follows this decision tree:

```
For each file:
├── Is filename all numbers (e.g., "20240312") OR starts with "Untitled"?
│   ├── YES → File needs renaming
│   │   ├── Does file have an H1 title?
│   │   │   ├── YES, and title is NOT "Untitled*" → Use title as filename
│   │   │   ├── YES, but title starts with "Untitled" → Replace title with first 5 words, then use as filename
│   │   │   └── NO → Use first 5 words of content as both title and filename
│   │   └── Sanitize filename (remove special chars, replace spaces with hyphens)
│   └── NO → File keeps current name
│       └── Does file have an H1 title?
│           ├── YES → No changes needed
│           └── NO → Add filename as H1 title
```

**Special Cases**:
- If title starts with "Untitled" → Replace with first 5 words of content
- Empty files → Skip with warning
- Target filename already exists → Skip with warning
- Special characters in titles → Sanitized for valid filenames

### Empty File Detection Rules (`delete-empty-files.md`)

A file is considered empty when:
1. File size < 150 bytes (configurable)
2. OR after removing all formatting/metadata, content < 20 characters

**What gets removed during detection**:
- Frontmatter (YAML between `---`)
- All headings (but their content is kept)
- Metadata lines ("Created at:", "Modified:", etc.)
- Empty list items (`- `, `* `, `1. `)
- Horizontal rules (`---`, `***`)
- Empty code blocks
- Excessive whitespace

## 🚀 How to Use

### Prerequisites
1. Install [Templater plugin](https://github.com/SilentVoid13/Templater) in Obsidian
2. Configure Templater settings:
   - Settings → Templater → Template folder location
   - Enable "Trigger Templater on new file creation" (optional)

### Installation
1. Download the scripts from this repository
2. Place them in your Templater templates folder (e.g., `Vault/Templates/`)
3. Scripts are now available via Templater

### Running the Scripts

#### Method 1: Direct Execution (Recommended)
1. Open the template file directly in Obsidian
2. Press `Cmd/Ctrl + P` to open command palette
3. Run "Templater: Replace templates in the active file"
4. Follow the interactive prompts

#### Method 2: Insert Template
1. Create a new temporary note
2. Press `Cmd/Ctrl + P` to open command palette
3. Run "Templater: Insert template"
4. Select the desired script
5. Follow the interactive prompts

#### Method 3: Hotkey (For Frequent Use)
1. Settings → Hotkeys
2. Search for "Templater: Insert"
3. Find your template and assign a hotkey
4. Use hotkey to run instantly

### Workflow Examples

#### Clean Up Weekly Captures
```
1. Run batch-rename-titles.md in Preview mode
2. Review planned changes in the report
3. Apply changes if satisfied
4. Run delete-empty-files.md to find empty Untitled files
5. Review and delete
```

#### Process Zettelkasten Notes
```
1. Run batch-rename-titles.md
2. Select "Process only Zettelkasten files"
3. Preview changes
4. Apply to convert numeric IDs to descriptive names
```

#### Clean Specific Folder
```
1. Run batch-rename-titles.md
2. Select "Select specific folder"
3. Choose your target folder (e.g., "Inbox")
4. Preview and apply
```

## ⚙️ Configuration

### Batch Rename Configuration
Edit these values in `batch-rename-titles.md`:

```javascript
const config = {
    excludeFolders: ['Templates', '.trash', '.obsidian', 'Archive'],
    batchSize: 10,              // Files processed simultaneously
    createBackupList: true      // Create file list before processing
};
```

### Empty File Detection Configuration
Edit these values in `delete-empty-files.md`:

```javascript
const config = {
    maxSizeBytes: 150,          // Files smaller = empty candidate
    maxContentChars: 20,        // Max chars after cleaning to be "empty"
    excludeFolders: ['Templates', '.trash', '.obsidian']
};
```

## 📊 Understanding the Reports

Each operation generates a detailed report including:

### Preview Reports Show
- Files that will be changed
- Specific modifications planned
- Files that will be skipped (with reasons)
- Folders being processed

### Completion Reports Show
- Total files processed
- Successful operations count
- Errors encountered
- Time elapsed
- Backup file location (if created)

### Example Report Structure
```markdown
# Batch Processing Report

## Summary
- Files Scanned: 1,234
- Files Renamed: 45
- Titles Added: 78
- "Untitled" Titles Replaced: 23
- Files Skipped: 12
- Errors: 0
- Time Elapsed: 4.56 seconds

## Planned Changes
### Inbox/Untitled-5.md
- Replace title: "Untitled" → "Meeting notes from quarterly review"
- Rename file: Inbox/Untitled-5.md → Inbox/Meeting-notes-from-quarterly-review.md
```

## 🛡️ Safety Features

1. **Never Destructive**: Original files preserved until you confirm changes
2. **Incremental Processing**: Handles files in batches to prevent system overload
3. **Error Recovery**: Continues processing even if individual files fail
4. **Detailed Logging**: Every action logged in timestamped reports
5. **Exclusion Lists**: Protected folders never touched
6. **Conflict Detection**: Won't overwrite existing files

## 🤝 Contributing

Feel free to submit issues or pull requests to improve these scripts.

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details

## 👤 Author

Created for the Obsidian community to manage growing vaults with Templater plugin.

## 🙏 Acknowledgments

- [Templater Plugin](https://github.com/SilentVoid13/Templater) by SilentVoid13
- Obsidian community for feedback and testing
