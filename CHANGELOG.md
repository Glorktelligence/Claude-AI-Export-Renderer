# Changelog

All notable changes to the Claude AI Export Renderer will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
