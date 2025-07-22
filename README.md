# AT Protocol Bookmark Lexicon

A comprehensive lexicon specification for building decentralized bookmark management systems on the AT Protocol.

## Overview

This repository contains the official lexicon definitions for the `app.hyber-limit` bookmark system, enabling users to:

- 📌 Save and organize web bookmarks with full data ownership
- 🔒 Create private, encrypted bookmarks with client-side encryption
- 👥 Share bookmarks through collaborative lists
- 🌐 Publish curated bookmark collections
- 🔗 Embed bookmarks in social posts
- 📁 Organize bookmarks in hierarchical folders

## Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/at-protocol-bookmark-lexicon.git
cd at-protocol-bookmark-lexicon

# Install dependencies (for development)
npm install
```

### Lexicon Files

The core lexicon definitions are located in the `lexicons/` directory:

- `app.hyber-limit.bookmark.json` - Core bookmark record type
- `app.hyber-limit.bookmark.list.json` - List/folder organizational structure  
- `app.hyber-limit.bookmark.embed.json` - Embed type for bookmark previews

### Basic Usage

```typescript
// Create a bookmark
const bookmark = {
  $type: 'app.hyber-limit.bookmark',
  url: 'https://example.com',
  title: 'Example Website',
  tags: ['example', 'demo'],
  createdAt: new Date().toISOString()
};

// Create a list
const list = {
  $type: 'app.hyber-limit.bookmark.list',
  name: 'My Reading List',
  visibility: 'private',
  createdAt: new Date().toISOString()
};
```

See [examples/usage-examples.md](examples/usage-examples.md) for comprehensive code examples.

## Features

### Bookmark Management
- Save URLs with titles, descriptions, and tags
- Add personal notes (up to 10,000 characters)
- Pin important bookmarks
- Archive old bookmarks
- Set reminders for later reading
- Track bookmark source when saved from others

### Privacy & Security
- Client-side encryption for sensitive bookmarks
- Private lists visible only to owner
- Granular permission controls for collaborative lists

### Social Features
- Like and comment on public bookmarks
- Share bookmarks to your feed
- Follow other users' bookmark collections
- Suggest bookmarks to public lists

### Organization
- Create hierarchical folder structures
- Assign bookmarks to multiple lists
- Color-code and icon-tag lists
- Import/export from browser formats

## Documentation

- [Business Requirements](docs/business-requirements.md) - Detailed feature specifications
- [Usage Examples](examples/usage-examples.md) - Code examples and patterns
- [CLAUDE.md](CLAUDE.md) - Development guidance for Claude Code

## Development

### Validate Lexicons

```bash
npm run validate
```

### Generate TypeScript Types

```bash
npm run generate-types
```

## Project Structure

```
at-protocol-bookmark-lexicon/
├── lexicons/              # Lexicon JSON definitions
├── docs/                  # Documentation
├── examples/              # Usage examples
├── schemas/               # Validation tests
├── types/                 # Generated TypeScript types
└── scripts/               # Build and validation scripts
```

## Contributing

Contributions are welcome! Please read our contributing guidelines and submit pull requests for any improvements.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Resources

- [AT Protocol Documentation](https://atproto.com/docs)
- [Lexicon Specification](https://atproto.com/specs/lexicon)
- [Bluesky Social](https://bsky.social)
