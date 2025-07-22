# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an AT Protocol lexicon specification repository for a decentralized bookmark management system. The project defines lexicon schemas for bookmarks that can be used within the AT Protocol ecosystem (Bluesky/atproto).

## Project Structure

The repository currently contains design documents but no implemented lexicon files yet. The planned structure based on initial.md:

```
at-protocol-bookmark-lexicon/
├── lexicons/                    # JSON lexicon definitions
│   ├── app.hyper-limit.bookmark.json
│   ├── app.hyper-limit.bookmark.list.json
│   └── app.hyper-limit.bookmark.embed.json
├── docs/                        # Documentation
├── examples/                    # Usage examples
└── schemas/                     # Validation tests
```

## Key Lexicons

The project defines three main lexicon types under the `app.hyper-limit` namespace:

1. **app.hyper-limit.bookmark** - Core bookmark record containing URL, title, description, tags, etc.
2. **app.hyper-limit.bookmark.list** - Organizational structure for folders and collaborative/public lists
3. **app.hyper-limit.bookmark.embed** - Custom embed type for bookmark previews in posts

## Architecture & Design

### Core Concepts

- **Data Sovereignty**: Users own their bookmark data through AT Protocol's decentralized architecture
- **Privacy Features**: Support for client-side encrypted bookmarks with `encrypted: true` flag
- **Social Features**: Integration with AT Protocol's like/reply/repost mechanisms
- **List Types**: Private (owner only), Collaborative (specific users), and Public (anyone can view)

### Key Technical Details

- Bookmarks reference lists via AT-URIs in the `listUris` array
- Maximum limits: 2048 chars for URLs, 300 for titles, 20 tags per bookmark
- Blob storage for preview images (max 500KB)
- Hierarchical list organization through `parent` field references

## Development Tasks

Since this is a specification project without build tools yet, the main development tasks involve:

1. Creating the JSON lexicon files from the schemas in brd.md
2. Setting up validation for the lexicon schemas
3. Creating TypeScript type definitions from the lexicons
4. Writing usage examples and documentation

## Working with AT Protocol Lexicons

When creating or modifying lexicon files:
- Follow AT Protocol lexicon specification format
- Ensure proper versioning (lexicon: 1)
- Use appropriate field types and constraints
- Consider backward compatibility for any changes

## Notes

- The project is in early stages - currently only documentation exists
- The JSON schemas are embedded in brd.md:220-418 and need to be extracted
- No package.json or build tools are set up yet
- Consider using AT Protocol's lexicon validation tools when implementing