# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Claude AI Export Renderer is a single-file web application that allows users to view, search, and explore their Claude conversation exports. The entire application is contained in `claude-export-renderer.html` - a standalone HTML file with embedded CSS and JavaScript.

**Important**: This is NOT affiliated with Anthropic PBC. It's a community-created tool that respects Anthropic's intellectual property rights. See README.md for full legal disclaimers.

## Architecture

### Single-File Design
The application uses a monolithic architecture where everything (HTML structure, CSS styling, JavaScript logic, and i18n translations) is embedded in one file for maximum portability. There is no build process, no dependencies, and no external files.

### Core Components

1. **ConversationRenderer Class** (main app controller)
   - State management: tracks conversations, filtered results, pagination state
   - File processing: handles JSON parsing and format normalization
   - Rendering pipeline: converts data to DOM elements
   - Event handling: search, filters, pagination, language switching

2. **Data Normalization Layer**
   - `processConversations()`: Handles multiple export format variations
   - `extractTextContent()`: Recursively extracts text from nested content structures
   - `formatMessageContent()`: Transforms content into HTML with artifact support
   - Filters out corrupted/empty conversations automatically

3. **Artifact Rendering System**
   - Detects tool use patterns in message content
   - Special rendering for code blocks, markdown, HTML artifacts
   - Visual indicators (icons, headers, syntax highlighting)
   - Located in `formatParsedContent()` and `formatMessageContent()`

4. **Internationalization (i18n)**
   - Translation dictionaries embedded as JavaScript objects (lines ~609-790)
   - Supports: English (default), German, Spanish, French
   - Auto-detection from browser language
   - `setLanguage()` updates all elements with `data-i18n` attributes
   - Preference persisted in localStorage

5. **Performance Optimization**
   - Adaptive pagination: 50/20/10 conversations per page based on dataset size
   - Large file detection (500+ conversations triggers warnings)
   - Memory-efficient rendering (only current page in DOM)
   - Dual pagination controls (top/bottom) for UX

## Key Features & Implementation

### Export Format Handling
The app handles multiple JSON structures from different Claude export versions:
- Array of conversations: `[{...}, {...}]`
- Wrapped format: `{conversations: [...]}`
- Data wrapper: `{data: [...]}`

See `processConversations()` at line ~919 for normalization logic.

### Search & Filtering
- Full-text search across conversation titles and message content
- Date range filters (today, week, month, quarter, year)
- Content filters (has Claude responses, long conversations 10+)
- Sort options (date, title, message count - ascending/descending)
- All filtering happens client-side in `applyFilters()` method

### Message Content Types
The renderer handles complex nested content structures:
- Plain text strings
- Arrays of mixed content (text + tool use)
- Tool use objects with artifacts
- Markdown and HTML content
- Tool results

Content extraction logic in `extractTextContent()` (line ~1288) and `extractFromParsedContent()` (line ~1312).

## Development Workflow

### Testing Changes
1. Edit `claude-export-renderer.html`
2. Open the file in a browser (Chrome recommended)
3. Test with various conversation export files:
   - Small exports (< 100 conversations)
   - Large exports (500+ conversations)
   - Different export format versions
   - Exports with artifacts, code blocks, tool use
4. Check browser console (F12) for JavaScript errors
5. Test all filter combinations and pagination
6. Verify language switching works correctly

### Browser Compatibility
Must support: Chrome, Firefox, Safari, Edge. Uses standard JavaScript (no transpilation), CSS Grid/Flexbox, and FileReader API.

### Privacy & Security
**Critical**: The application must NEVER:
- Send data to external servers
- Load external resources/CDNs
- Include analytics or tracking
- Require internet connection

All processing happens locally in the browser. This is a core design principle.

## Common Modifications

### Adding a New Language
1. Add translation object to `translations` constant (line ~609)
2. Add `<option>` to language selector in HTML (line ~500)
3. Ensure all UI strings have corresponding keys in translation object
4. Test auto-detection and manual switching

### Changing Pagination Defaults
Modify thresholds in `showInterface()` method (line ~991):
- Line ~1004: Large file threshold (500 conversations → 10 per page)
- Line ~1015: Medium file threshold (100 conversations → 20 per page)
- Line ~1017: Small file default (50 per page)

### Adding New Filters
1. Add filter UI element in controls section (line ~515)
2. Implement filter logic in `applyFilters()` method
3. Update filter change event handlers to call `renderConversations()`
4. Add translations for new filter labels

## File Structure Notes

There are no source files to compile. The project structure is:
- `claude-export-renderer.html` - The entire application
- `README.md` - User documentation
- `CHANGELOG.md` - Version history
- `SECURITY.md` - Security policy and vulnerability reporting
- `LICENSE` - MIT license with trademark acknowledgments
- `VERSION` - Current version number

## Version History

- **v1.0.1**: Added multilingual support (EN, DE, ES, FR) with auto-detection
- **v1.0.0**: Initial release with search, filtering, pagination, artifact rendering

## Important Constraints

1. **Single-file requirement**: All changes must remain in one HTML file
2. **No external dependencies**: No npm packages, no CDN resources
3. **No build process**: Must work by simply opening the HTML file
4. **Backward compatibility**: Should handle old conversation export formats
5. **Performance**: Must handle 32MB+ files without browser crashes
6. **Privacy-first**: No data leaves the user's browser
