# Mission Control — Personal Knowledge Management System

A lightweight, self-contained 2nd brain for organizing documents, research, and contacts with zero dependencies.

## What is it?

Mission Control is a personal knowledge atlas—a single HTML file that serves as your central hub for:
- **Documents**: Journal entries, research notes, concept documentation
- **Contacts**: People directory with email, relationship, and notes
- **Filtering & Search**: Tag-based filtering and full-text search across all documents

Think of it as a personal wiki meets contact manager, with a beautiful dark UI optimized for long reading sessions.

## What It Does

### Core Features

- **📖 Document Viewer**: Render markdown-formatted notes with proper typography
- **🏷️ Tag System**: Organize documents with multiple tags; filter by tag or search
- **👥 Contact Directory**: Maintain a directory of important contacts with email and relationship info
- **📝 Document Types**: Automatically separates "Journal" (dated daily notes) from "Concepts" (evergreen research/ideas)
- **🔍 Search**: Real-time search across document titles and content
- **🌙 Dark Theme**: Eye-friendly dark UI with blue accents (Tailwind-inspired colors)
- **📱 Responsive**: Works on desktop and tablet

### No External Dependencies

- Pure HTML + Vanilla JavaScript
- No build step, no npm install
- Single `index.html` file runs everywhere
- Can be served over HTTP or opened locally

## How It Was Built

### Architecture

**Single HTML File**
```
mission-control/
├── index.html          # Everything: HTML, CSS, JavaScript
└── README.md           # This file
```

All documents and contacts are embedded as JavaScript arrays inside the HTML file:

```javascript
const docs = [
  {
    slug: "journal/2026-02-13",
    title: "Document Title",
    date: "2026-02-13",
    tags: ["journal", "daily"],
    content: "# Markdown content here..."
  }
];

const contacts = [
  {
    name: "Kate Mangan",
    email: "kate@example.com",
    relationship: "Wife",
    notes: "Auberge Resorts"
  }
];
```

### Technology Stack

- **HTML5**: Structure and semantic markup
- **CSS3**: Flexbox layout, CSS Grid (for people cards), custom properties for theming
- **Vanilla JavaScript**: No frameworks; pure DOM manipulation and event listeners
- **Markdown Rendering**: Basic regex-based markdown parser (headings, lists, bold, code)

### Design Decisions

1. **Self-Contained**: Single file = easy backup, easy share, no server needed
2. **No Build**: Edit HTML directly, refresh browser, done
3. **Markdown Support**: Human-readable format; easy to copy content in/out
4. **Dark Theme**: Default to dark with blue accents (#3b82f6) for reduced eye strain
5. **Tag-First Organization**: Instead of folders/hierarchy, tags allow flexible cross-cutting organization

### UI Components

- **Sidebar**: Document list, search, tag filtering, people search
- **Tab System**: Switch between Documents and People views
- **Document Header**: Title, tag pills, date
- **Document Body**: Markdown-rendered content
- **Contact Cards**: Stacked cards with name, email, relationship, notes
- **Tag Pills**: Clickable tags for filtering

## Usage

### Opening the App

**Option 1: Local File**
```bash
open /Users/cora/.openclaw/workspace/mission-control/index.html
```

**Option 2: HTTP Server**
```bash
cd /Users/cora/.openclaw/workspace/mission-control
python3 -m http.server 8000
# Then visit http://localhost:8000
```

**Option 3: Live URL** (if deployed)
```
https://mission-control.example.com
```

### Adding Documents

Edit the `docs` array in `index.html`:

```javascript
{
  slug: "journal/YYYY-MM-DD",      // Unique ID; / creates hierarchy in sidebar
  title: "Your Title",              // Display name
  date: "YYYY-MM-DD",               // Optional; omit for concepts
  tags: ["journal", "topic"],       // Array of tags
  content: "# Markdown here..."      // Full markdown support
}
```

**Tag Conventions**:
- `"journal"` — Automatically grouped under "Journal" section (add a date)
- `"daily"` — Personal daily logs
- `"concept"` — Evergreen research/ideas (goes under "Concepts" section)
- Custom tags — Any topic tag (e.g., "linkedin", "marketing", "automation")

### Adding Contacts

Edit the `contacts` array:

```javascript
{
  name: "Person Name",
  email: "person@example.com",
  relationship: "Title/Relationship",    // Optional (e.g., "Wife", "Developer")
  notes: "Additional context"            // Optional (e.g., "Auberge Resorts")
}
```

### Search & Filter

- **Search Box** (Docs tab): Type to search document titles in real-time
- **Tag Pills**: Click any tag to filter; click "All" to clear
- **People Search** (People tab): Search by name or email

## Markdown Support

The built-in markdown parser supports:
- `# Heading 1`, `## Heading 2`, `### Heading 3`
- `- List item` (converts to `<ul>`)
- `1. Ordered item` (converts to `<ol>`)
- `**bold text**`
- `` `inline code` ``
- Paragraphs (separated by blank lines)

**Unsupported**: Links, images, tables, code blocks with syntax highlighting (can be added if needed).

## Why This Approach?

After trying the full Next.js version (with lucide-react, Tailwind, TypeScript), we discovered:
- **React hydration issues** on Safari (client-side fetch not firing)
- **Build complexity** (npm dependencies, webpack, babel)
- **Over-engineering** for a simple knowledge base

The vanilla HTML version:
- ✅ Works instantly (no build, no Node)
- ✅ Loads in any browser (Safari, Chrome, Firefox)
- ✅ Easy to fork and modify
- ✅ Backed up to Git easily
- ✅ Can be printed or exported as HTML

## Future Enhancements

Possible additions (without breaking the single-file principle):

- LocalStorage: Persist edits without a backend
- Export to PDF: Print selected documents
- Dark/Light toggle: Add theme switching
- Full markdown parser: Support all markdown syntax
- Keyboard shortcuts: Quick navigation
- Code syntax highlighting: Better code block rendering
- Rich editor: Inline editing instead of editing HTML directly

## Git History

```
commit 6e2b009
Author: Cora <cora@berelvant.com>
Date:   Fri Feb 13 15:37 2026

    Initial commit: Mission Control 2nd brain UI
```

## Files

- **index.html** - Complete working app (387 lines)
- **README.md** - This documentation

## License

Personal project. Feel free to fork and modify for your own knowledge base.

---

**Built with**: HTML5 + CSS3 + Vanilla JS  
**Hosted**: [GitHub: cora-brlvnt/mission-control](https://github.com/cora-brlvnt/mission-control)  
**Created**: Feb 2026
