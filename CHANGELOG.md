# Changelog

All notable changes to the Claude AI Export Renderer will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Testing Deployment of Monitoring this Changelog - ZERO code changes

## [2.2.0] - 2026-04-05

### Added

- **Enhanced Markdown Rendering**: Full inline markdown parser replacing basic text rendering
  - Tables (`| col | col |` syntax) with dark-themed styling
  - Ordered and unordered lists (`1.`, `-`, `*`)
  - Blockquotes (`>`) with accent-colored left border
  - Horizontal rules (`---`, `***`)
  - Strikethrough (`~~text~~`)
  - Improved heading, bold, italic, link, and inline code rendering
- **Language-Specific Code Block Styling**: Color-tinted headers for 20+ languages
  - Python (blue), JavaScript (yellow), TypeScript (blue), JSON (green), HTML (orange), CSS (purple), SQL (cyan), YAML (grey), Rust (red), Go (cyan), and more
  - Diff syntax coloring (`+` green, `-` red, `@` cyan)
  - Bash/shell reuses existing terminal-block dark styling
- **Copy Button on Code Blocks**: One-click clipboard copy with "Copied!" feedback
  - Appears on every code block, tool input, and terminal block
  - `navigator.clipboard` API with `execCommand('copy')` fallback for older browsers
- **Statistics Dashboard**: Collapsible detailed statistics panel
  - Human/Assistant message breakdown
  - Longest conversation
  - Content type counts (tool use blocks, thinking blocks, code blocks, images)
  - Top 6 most-used tools with icons
  - Computed during import for both in-memory and IndexedDB modes
- **Keyboard Navigation**: Comprehensive keyboard shortcuts
  - `/` to focus search, `j`/`k` for next/prev conversation (vim-style)
  - `Home`/`End` for first/last page
  - `Enter` to toggle focused conversation
  - `Escape` to close modals or collapse expanded conversations
  - Updated shortcuts help modal with all new bindings
- **Print-Friendly CSS**: `@media print` styles for clean Ctrl+P output
  - Hides controls, pagination, export buttons, and modals
  - Forces expanded conversation content, white background
  - Avoids page breaks inside conversations
- **Export to Markdown**: New 📝 button on conversation headers
  - Converts conversation to markdown with headings, tool blocks, code, thinking summaries
  - Downloads as `.md` file using same Blob mechanism as JSON export
- **Conversation Word Count**: Estimated word count shown in conversation list headers
  - Computed during normalization for both in-memory and IndexedDB modes
  - Displayed as "~124,500 words" next to message count

### Improved

- **Theme Toggle**: Button now shows ☀️/🌙 icons, all hardcoded CSS colors replaced with CSS variables
  - Added `--btn-blue-bg`, `--btn-blue-hover`, `--warning-text`, `--disabled-bg`, `--disabled-text` variables
  - Both dark and light theme definitions updated
- **localStorage Safety**: All localStorage calls wrapped in `safeStorage` with try/catch and in-memory fallback
  - Shows subtle notice when storage unavailable (e.g., `file://` protocol)
  - Settings, theme, and language preferences gracefully degrade

### Technical Details

- Single-file architecture maintained (~4,700+ lines)
- Markdown parser handles tables, lists, and blockquotes without external libraries
- Stats computed during initial processing (streaming accumulator for IDB mode)
- No external dependencies added

## [2.1.0] - 2026-04-05

### Added

- **Smart Loading with IndexedDB**: Files over 10MB are now streamed and stored in IndexedDB instead of loaded entirely into memory
  - `StreamingJSONArrayParser`: Reads files in 1MB chunks, tracks JSON nesting depth, parses each conversation object individually — never loads the whole file at once
  - `ConversationDB`: Full IndexedDB wrapper with conversations/messages/metadata stores, cursor-based pagination, full-text search, and stats queries
  - Handles all three Claude export formats (direct array, `{conversations:[...]}`, `{data:[...]}`) via streaming
- **Lazy Message Loading**: In IndexedDB mode, messages load only when a conversation is expanded — keeps memory under 5MB regardless of export size
- **Progress Bar UI**: Proper progress bar during large file import showing percentage, conversation count, file size processed, and elapsed time
- **Dual-Mode Architecture**: Files under 10MB use the existing fast in-memory path (unchanged); files over 10MB use the IndexedDB streaming path

### Improved

- **Conversation Normalization**: Extracted `normaliseConversation()` method shared by both in-memory and IndexedDB import paths
- **Search in IndexedDB Mode**: Full-text search across conversation names and message content via IDB cursor scan with search progress indicator
- **Filters in IndexedDB Mode**: Date range, has-assistant, long conversations, and recent filters all work from lightweight conversation headers stored in memory (~2MB for 10K conversations)
- **Exports in IndexedDB Mode**: All export functions (filtered, selected, individual) reconstruct full conversations from IndexedDB on demand

### Technical Details

- Single-file architecture maintained (~4,200 lines)
- IndexedDB schema: 3 stores (conversations, messages, metadata) with indexes for sorting
- Conversation headers loaded into memory for fast filtering; messages lazy-loaded from IDB
- Streaming parser handles escaped strings, nested objects, and multi-chunk boundaries correctly
- No external dependencies added

## [2.0.0] - 2026-04-05

### Added

- **Content Block Rendering System**: Complete overhaul of how Claude message content is displayed
  - Messages with typed content arrays (text, tool_use, tool_result, thinking, image) are now rendered with dedicated block renderers instead of plain text
  - New `renderMessageContent()` dispatcher detects string vs array content and routes to the appropriate renderer
  - New `renderContentBlock()` switch handles all known block types with specialized display
- **Tool Use Rendering**: Rich visual display for all Claude tool invocations
  - Icon and display name mapping for 20 known tools (web_search, bash_tool, str_replace, etc.)
  - Collapsible tool blocks with descriptive headers (collapsed by default)
  - Tool-specific input rendering:
    - `web_search`: Query display
    - `bash_tool`: Terminal-style dark block with green text and blue `$` prompt
    - `str_replace`: Diff-style display with red (removed) and green (added) lines
    - `create_file`: Filename header with collapsible code content
    - `view`: File path display with optional line range
    - `web_fetch`: Clickable URL link
    - Generic fallback: formatted JSON display
- **Tool Result Rendering**: Collapsible result blocks paired with their tool_use by `tool_use_id`
- **Thinking Block Rendering**: Extended thinking / chain-of-thought blocks
  - Collapsed by default with estimated token count (~chars/4) in header
  - Italic styling to distinguish from regular content
- **Image Block Rendering**: Inline base64 image display with lazy loading
- **Global Toggle Function**: `toggleToolBlock()` for all collapsible content blocks
- **Comprehensive CSS**: New styles for `.tool-use-container`, `.tool-result-container`, `.thinking-container`, `.terminal-block`, `.diff-block`, `.image-block` with light theme overrides

### Improved

- **Search Extraction**: `extractTextContent` now handles thinking blocks and image placeholders for full-text search across all content types
- **Artifact Preservation**: Existing artifact rendering (tool_use with name='artifacts') is preserved through dedicated `renderArtifactBlock()` method

### Technical Details

- Single-file architecture maintained (~3,500+ lines)
- All new rendering uses existing CSS variable system for theme compatibility
- Content block rendering coexists with legacy string content formatting
- No external dependencies added

## [1.0.2] - 2025-10-26

### Added

- **Complete Export System**: Comprehensive conversation export functionality with multiple options
  - Export filtered conversations with proper JSON formatting
  - Export selected conversations with bulk selection tools
  - Export individual conversations with hover button (💾 icon)
- **Selection Mode**: Toggle-based selection system with progressive disclosure
  - Enable/Disable Selection Mode button
  - Individual conversation checkboxes
  - Bulk actions bar with selection count
- **Bulk Selection Tools**:
  - Select All (all filtered conversations)
  - Select All Visible (current page only)
  - Clear Selection
- **Export Settings Modal**: Fully customizable export preferences
  - Date format options (YYYY-MM-DD, DD-MM-YYYY, MM-DD-YYYY, or no date)
  - Max title length in filename (20-100 characters)
  - JSON indentation (2 or 4 spaces)
  - Timestamp inclusion toggle
  - Settings persistence with localStorage
  - Reset to defaults functionality
- **Export Progress Indicators**: Visual feedback during export operations
  - Animated spinner overlay
  - Status text with conversation count
  - Auto-dismiss on completion
  - Error handling with user-friendly messages
- **Collapsible Code Sections**: Improved readability for long conversations
  - Collapsible artifacts (default: collapsed)
  - Collapsible code blocks (default: collapsed)
  - Language labels for code blocks
  - Smooth expand/collapse animations

### Improved

- **File Naming Conventions**: Smart, customizable filename generation
  - Sanitized conversation titles in filenames
  - Configurable date formats
  - Optional timestamps
  - Prevents overly long filenames
- **User Experience**: Enhanced interface and workflow
  - Hover-activated export buttons (minimal footprint)
  - Settings gear icon (⚙️) next to language selector
  - Click outside to close modal
  - Clear visual feedback for all actions

### Technical Details

- Single-file architecture maintained (~2,500 lines)
- Export format maintains compatibility with Anthropic's JSON structure
- All processing remains client-side (no external dependencies)
- Settings stored in browser localStorage
- Proper JSON indentation (user-configurable)
- File naming sanitization for cross-platform compatibility
- Progress indicators use setTimeout for non-blocking UI updates
- Full i18n support for all new features (EN, DE, ES, FR)

## [1.0.1] - 2025-10-23

### Added

- **Multilingual Support System**: Complete internationalization support with automatic browser language detection
- **Language Selector**: Dropdown in header for manual language switching
- **Language Persistence**: Remembers user's language preference in browser localStorage
- **Supported Languages**:
  - English (Default)
  - Deutsch (German)
  - Español (Spanish)
  - Français (French)
- **Auto-detection**: Automatically detects browser language on first visit
- **Complete Translation Coverage**: All interface elements, buttons, labels, placeholders, and footer content

### Technical Details

- Single-file architecture maintained - no additional files required
- Translations embedded as JavaScript objects (~15KB overhead)
- Instant language switching without page reload
- All conversation content remains in original user language

## [1.0.0] - 2025-10-23

### Added

- **Initial Release**: Core Claude conversation export viewing functionality
- **File Support**: Handles large JSON export files (tested with 32MB+ files)
- **Search System**: Full-text search across conversation titles and message content
- **Advanced Filtering**:
  - Sort by date, title, or message count
  - Filter by date ranges (today, week, month, quarter, year)
  - Show only conversations with Claude responses
  - Filter for long conversations (10+ messages)
- **Artifact Rendering**: Proper display of code blocks, markdown, and generated content
- **Pagination System**:
  - Adaptive page sizes (10-50 conversations per page)
  - Dual pagination controls (top and bottom)
  - Large file detection and optimization
  - Smooth scrolling between pages
- **Statistics Dashboard**: Total conversations, messages, date range, and averages
- **Performance Features**:
  - Handles corrupted "[object Object]" entries automatically
  - Memory-efficient rendering for large datasets
  - Browser-only processing (no external dependencies)
- **User Experience**:
  - Dark theme with clean interface
  - Responsive design for mobile devices
  - Auto-hiding notifications with smooth transitions
  - Collapsible conversation view
- **Privacy & Security**:
  - Completely local processing
  - No data transmission
  - No external dependencies
  - Offline capable

### Security

- Added comprehensive security policy (SECURITY.md)
- Professional contact channels for vulnerability reporting
- Privacy-first architecture with local-only data processing

### Documentation

- Complete README.md with installation and usage instructions
- Legal disclaimers respecting Anthropic's intellectual property
- MIT License with trademark acknowledgments
- Professional support contact information

## Future Considerations

### Potential Features

- Additional language support based on user feedback
- Export functionality for filtered conversations
- Conversation analytics and statistics
- Dark/light theme toggle
- Advanced search capabilities (regex, date ranges)
- Import/export of search filters and preferences

---

**Note**: This project respects Anthropic's intellectual property and is not affiliated with Anthropic PBC. See README.md for full legal disclaimers.

**Note**: Testing new monitoring function for discord community on this file!
