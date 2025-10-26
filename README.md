
# Claude AI Export Renderer

A web-based tool for viewing and exploring Claude conversation exports with search, filtering, pagination, artifact rendering, and comprehensive export functionality.

## Recent Updates

**Version 1.0.2** - Major update adding comprehensive export functionality with customizable settings, selection tools, and collapsible code sections. Export filtered conversations, selected conversations, or individual conversations with full control over file naming and formatting. See [CHANGELOG.md](https://github.com/Glorktelligence/Claude-AI-Export-Renderer/blob/main/CHANGELOG.md) for full version history.

## Legal Disclaimer

 **IMPORTANT** : This project is an independent, community-created tool and is not affiliated with, endorsed by, or sponsored by Anthropic PBC. "Claude" and "Claude AI" are trademarks of Anthropic PBC. This tool is designed to work with data exports from Claude AI conversations that users have legitimately obtained from their own accounts.

This project respects Anthropic's intellectual property rights and trademarks. The use of "Claude" in the project name is solely for descriptive purposes to indicate compatibility with Claude conversation exports. Users are responsible for ensuring they have the right to use any conversation data with this tool and must comply with Anthropic's Terms of Service and applicable laws.

If you are a representative of Anthropic PBC and have concerns about this project, please contact us at support@glorktelligence.co.uk - we are committed to working collaboratively to address any issues.

## Features

* **Clean Interface** : Dark theme with intuitive navigation
* **Search & Filter** : Find specific conversations and messages instantly
* **Comprehensive Export System** : Export filtered, selected, or individual conversations with customizable settings
* **Selection Tools** : Bulk selection with checkboxes and selection helpers
* **Export Settings** : Customize file naming, date formats, JSON indentation, and more
* **Collapsible Code Sections** : Artifacts and code blocks collapse by default for cleaner viewing
* **Artifact Rendering** : Properly displays code, markdown, and generated content
* **Pagination** : Handles large exports efficiently (tested with 32MB+ files)
* **Performance Optimized** : Won't crash your browser with large conversation histories
* **Responsive Design** : Works on desktop and mobile devices
* **Multilingual Support** : Complete interface translation with automatic language detection

## Internationalization

The Claude AI Export Renderer supports multiple languages with automatic browser detection and manual switching:

* **English** (Default)
* **Deutsch** (German)
* **Español** (Spanish)
* **Français** (French)

The language selector in the top-right corner allows instant switching between languages. Your language preference is automatically saved and the interface will remember your choice on future visits. All conversation content remains in its original language while the interface adapts to your preferred language.

## Quick Start

1. Download the `claude-export-renderer.html` file
2. Open it in any modern web browser
3. Click "Choose Claude Export File" and select your `conversations.json`
4. Explore your conversations with search, filters, and pagination
5. Use the export features to save filtered or selected conversations
6. Customize export settings via the ⚙️ settings icon

## How to Get Your Claude Export

1. Go to Claude.ai
2. Navigate to Settings → Data Export
3. Request your conversation export
4. Download the `conversations.json` file when ready
5. Use this tool to view it in a readable format

## Browser Compatibility

* Chrome/Chromium (recommended)
* Firefox
* Safari
* Edge

## Features in Detail

### Search Functionality

* Press Enter or click Search to find conversations
* Searches both conversation titles and message content
* Highlights matching terms in results

### Filtering Options

* Sort by date, title, or message count
* Filter by date ranges (today, week, month, etc.)
* Show only conversations with Claude responses
* Filter long conversations (10+ messages)

### Artifact Support

* Properly renders code blocks with syntax highlighting
* Displays markdown content with formatting
* Shows HTML and JavaScript artifacts in code blocks
* Tool use displays with clear indicators
* **NEW**: Artifacts and code blocks are collapsible (collapsed by default)
* Click headers to expand/collapse content for cleaner reading

### Export Functionality

The tool offers three ways to export conversations:

* **Export Filtered Conversations**: Export all conversations matching your current search/filter criteria
* **Export Selected Conversations**: Use selection mode to pick specific conversations, then export them
* **Export Individual Conversation**: Hover over any conversation header and click the 💾 icon to export just that one

All exports maintain compatibility with Anthropic's JSON format and can be re-imported into the tool.

### Selection Mode

* Click "Enable Selection Mode" to show checkboxes on conversation headers
* Select individual conversations by clicking checkboxes
* Use "Select All" to select all filtered conversations (across all pages)
* Use "Select All Visible" to select only conversations on the current page
* Use "Clear Selection" to deselect all
* Selection count displayed in the bulk actions bar
* Export your selection with the "Export Selected" button

### Export Settings

Click the ⚙️ settings icon (next to language selector) to customize exports:

* **Date Format**: Choose YYYY-MM-DD, DD-MM-YYYY, MM-DD-YYYY, or no date
* **Include Timestamp**: Optionally add time to filename (e.g., 2024-10-26-14-30)
* **Max Title Length**: Control how many characters from the conversation title appear in filename (20-100)
* **JSON Indentation**: Choose 2 or 4 spaces for formatting
* Settings are automatically saved and persist across sessions
* Reset to defaults option available

### Performance Features

* Adaptive pagination (10-50 conversations per page)
* Large file detection and optimization
* Smooth scrolling between pages
* Auto-hiding notifications

## File Size Support

The tool handles exports of various sizes:

* Small exports (< 100 conversations): 50 per page
* Medium exports (100-500 conversations): 20 per page
* Large exports (500+ conversations): 10 per page
* Shows performance warnings for very large files

## Privacy & Security

* **No data transmission** : Everything runs locally in your browser
* **No external dependencies** : Single HTML file with embedded CSS/JS
* **No tracking** : No analytics or external connections
* **Offline capable** : Works without internet connection

## Technical Details

* Pure HTML/CSS/JavaScript - no frameworks required (~2,500 lines)
* Handles complex Claude export formats including tool use and artifacts
* Filters out corrupted "[object Object]" entries automatically
* Memory-efficient pagination for large datasets
* Responsive design with mobile support
* Export format maintains full compatibility with Anthropic's JSON structure
* Settings persistence via browser localStorage
* Progress indicators for export operations
* File naming sanitization for cross-platform compatibility

## Known Limitations

* Very large files (100MB+) may take time to initially process
* Search is case-insensitive and uses simple text matching
* Some very old or corrupted conversation entries may not display properly

## Contributing

Issues and pull requests welcome! Areas for potential improvement:

* Additional language support based on community requests
* Enhanced search capabilities (regex, advanced filters)
* Additional export formats (CSV, Markdown, etc.)
* Conversation statistics and analytics dashboard
* Dark/light theme toggle
* Batch conversation management features

## Development

The entire application is contained in a single HTML file for maximum portability. To modify:

1. Edit `claude-export-renderer.html`
2. Test with various conversation export files
3. Ensure browser compatibility across major browsers

## License

MIT License - see LICENSE file for details.

## Changelog

For detailed version history, see [CHANGELOG.md](https://github.com/Glorktelligence/Claude-AI-Export-Renderer/blob/main/CHANGELOG.md).

### v1.0.2 (2025-10-26)

* Complete export system with 3 export options
* Selection mode with bulk selection tools
* Export settings modal with customizable preferences
* Export progress indicators
* Collapsible artifacts and code blocks
* Smart file naming with multiple date format options

### v1.0.1 (2025-10-23)

* Multilingual support (EN, DE, ES, FR)
* Automatic language detection
* Language preference persistence

### v1.0.0 (2025-10-23)

* Initial release
* Basic conversation viewing with search and filters
* Artifact rendering support
* Pagination for large files
* Performance optimizations

## Support

If you encounter issues:

1. Check the browser console (F12) for error messages
2. Verify your `conversations.json` file is valid JSON
3. Try with a smaller subset of conversations first
4. Contact us at support@glorktelligence.co.uk or open an issue with details about your export file size and browser

## Acknowledgments

Created by the Claude community for the Claude community. Thanks to all users who provided feedback and testing with various export file formats and sizes.
