# AT Protocol Bookmark System - Usage Examples

This document provides practical examples of using the bookmark lexicons in AT Protocol applications.

## Creating a Bookmark

### Basic Bookmark

```typescript
const bookmark = {
  $type: 'app.hyper-limit.bookmark',
  url: 'https://example.com/article',
  title: 'Interesting Article About AT Protocol',
  description: 'An in-depth look at decentralized social networks',
  tags: ['atproto', 'decentralized', 'web3'],
  pinned: false,
  archived: false,
  encrypted: false,
  createdAt: new Date().toISOString()
};

// Create the record
const response = await agent.api.com.atproto.repo.createRecord({
  repo: agent.session.did,
  collection: 'app.hyper-limit.bookmark',
  record: bookmark
});
```

### Bookmark with Image

```typescript
// Upload image first
const imageBlob = await agent.api.com.atproto.repo.uploadBlob(imageFile, {
  encoding: 'image/jpeg'
});

const bookmarkWithImage = {
  $type: 'app.hyper-limit.bookmark',
  url: 'https://example.com/visual-guide',
  title: 'Visual Guide to AT Protocol',
  description: 'Step-by-step visual tutorial',
  imageBlob: imageBlob.data.blob,
  tags: ['tutorial', 'guide'],
  createdAt: new Date().toISOString()
};
```

### Private Encrypted Bookmark

```typescript
// Client-side encryption of sensitive fields
const encryptedNote = await encryptText(personalNote, userKey);
const encryptedDescription = await encryptText(description, userKey);

const privateBookmark = {
  $type: 'app.hyper-limit.bookmark',
  url: 'https://private-resource.com',
  title: 'Private Resource', // Title remains unencrypted for listing
  description: encryptedDescription,
  note: encryptedNote,
  encrypted: true,
  createdAt: new Date().toISOString()
};
```

## Creating Lists

### Private List (Folder)

```typescript
const privateList = {
  $type: 'app.hyper-limit.bookmark.list',
  name: 'Work Resources',
  description: 'Tools and documentation for work',
  icon: 'folder',
  color: '#0066CC',
  visibility: 'private',
  createdAt: new Date().toISOString()
};

const listResponse = await agent.api.com.atproto.repo.createRecord({
  repo: agent.session.did,
  collection: 'app.hyper-limit.bookmark.list',
  record: privateList
});
```

### Public List

```typescript
const publicList = {
  $type: 'app.hyper-limit.bookmark.list',
  name: 'Best AT Protocol Resources',
  description: 'Curated collection of AT Protocol documentation and tools',
  icon: 'star',
  visibility: 'public',
  coverImage: coverImageBlob.data.blob,
  createdAt: new Date().toISOString()
};
```

### Collaborative List

```typescript
const collaborativeList = {
  $type: 'app.hyper-limit.bookmark.list',
  name: 'Team Resources',
  description: 'Shared bookmarks for our development team',
  visibility: 'collaborative',
  permissions: {
    canAdd: [
      'did:plc:teammate1',
      'did:plc:teammate2'
    ]
  },
  createdAt: new Date().toISOString()
};
```

## Adding Bookmarks to Lists

```typescript
// First create the list
const listUri = listResponse.uri;

// Then create bookmark with list reference
const bookmarkInList = {
  $type: 'app.hyper-limit.bookmark',
  url: 'https://example.com/resource',
  title: 'Useful Resource',
  listUris: [listUri], // Can belong to multiple lists
  createdAt: new Date().toISOString()
};
```

## Embedding Bookmarks in Posts

```typescript
// First, get the bookmark record
const bookmarkRecord = await agent.api.com.atproto.repo.getRecord({
  repo: agent.session.did,
  collection: 'app.hyper-limit.bookmark',
  rkey: bookmarkRkey
});

// Create a post with embedded bookmark
const post = {
  $type: 'app.bsky.feed.post',
  text: 'Check out this amazing resource I found!',
  embed: {
    $type: 'app.hyper-limit.bookmark.embed',
    bookmark: {
      uri: bookmarkRecord.uri,
      cid: bookmarkRecord.cid
    }
  },
  createdAt: new Date().toISOString()
};

await agent.api.com.atproto.repo.createRecord({
  repo: agent.session.did,
  collection: 'app.bsky.feed.post',
  record: post
});
```

## Querying Bookmarks

### List All Bookmarks

```typescript
const bookmarks = await agent.api.com.atproto.repo.listRecords({
  repo: agent.session.did,
  collection: 'app.hyper-limit.bookmark',
  limit: 50
});
```

### Filter by List

```typescript
// Get all bookmarks in a specific list
const listUri = 'at://did:plc:user/app.hyper-limit.bookmark.list/abc123';

const bookmarksInList = bookmarks.records.filter(record => 
  record.value.listUris?.includes(listUri)
);
```

### Search by Tags

```typescript
const tag = 'atproto';
const taggedBookmarks = bookmarks.records.filter(record =>
  record.value.tags?.includes(tag)
);
```

## Managing Hierarchical Lists

```typescript
// Create parent folder
const parentFolder = {
  $type: 'app.hyper-limit.bookmark.list',
  name: 'Development',
  visibility: 'private',
  createdAt: new Date().toISOString()
};

const parentResponse = await agent.api.com.atproto.repo.createRecord({
  repo: agent.session.did,
  collection: 'app.hyper-limit.bookmark.list',
  record: parentFolder
});

// Create child folder
const childFolder = {
  $type: 'app.hyper-limit.bookmark.list',
  name: 'JavaScript Resources',
  parent: parentResponse.uri, // Reference to parent
  visibility: 'private',
  createdAt: new Date().toISOString()
};
```

## Import Browser Bookmarks

```typescript
// Parse browser bookmarks HTML
const bookmarks = parseBrowserBookmarks(htmlContent);

// Create bookmarks in AT Protocol
for (const bookmark of bookmarks) {
  await agent.api.com.atproto.repo.createRecord({
    repo: agent.session.did,
    collection: 'app.hyper-limit.bookmark',
    record: {
      $type: 'app.hyper-limit.bookmark',
      url: bookmark.url,
      title: bookmark.title || 'Untitled',
      tags: bookmark.folders || [],
      createdAt: bookmark.dateAdded || new Date().toISOString()
    }
  });
}
```

## Handling Reminders

```typescript
const bookmarkWithReminder = {
  $type: 'app.hyper-limit.bookmark',
  url: 'https://example.com/read-later',
  title: 'Article to Read Later',
  reminder: {
    date: '2024-12-01T10:00:00Z',
    note: 'Review for upcoming presentation'
  },
  createdAt: new Date().toISOString()
};
```

## Social Features

### Saving from Another User

```typescript
// Reference the original bookmark
const savedBookmark = {
  $type: 'app.hyper-limit.bookmark',
  url: originalBookmark.url,
  title: originalBookmark.title,
  description: originalBookmark.description,
  sourceUri: originalBookmarkUri, // Reference to original
  createdAt: new Date().toISOString()
};
```

### Suggesting to Public List

```typescript
// Create a reply to the public list with bookmark suggestion
const suggestion = {
  $type: 'app.bsky.feed.post',
  text: 'I think this resource would be great for your list!',
  reply: {
    root: { uri: publicListUri, cid: publicListCid },
    parent: { uri: publicListUri, cid: publicListCid }
  },
  embed: {
    $type: 'app.hyper-limit.bookmark.embed',
    bookmark: {
      uri: suggestedBookmarkUri,
      cid: suggestedBookmarkCid
    }
  },
  createdAt: new Date().toISOString()
};
```

## Error Handling

```typescript
try {
  const response = await agent.api.com.atproto.repo.createRecord({
    repo: agent.session.did,
    collection: 'app.hyper-limit.bookmark',
    record: bookmark
  });
} catch (error) {
  if (error.status === 400) {
    console.error('Invalid bookmark data:', error.message);
  } else if (error.status === 403) {
    console.error('Permission denied');
  }
}
```

## Best Practices

1. **Always validate URLs** before creating bookmarks
2. **Use meaningful tags** for better organization
3. **Set appropriate visibility** for lists based on content
4. **Handle encryption keys securely** for private bookmarks
5. **Respect rate limits** when importing bulk bookmarks
6. **Cache bookmark data** locally for better performance
7. **Use strong references** when embedding bookmarks in posts