# Mission Control (2nd Brain)

A personal knowledge management system for documents, research, and contacts.

## Features

- 📖 Document viewer with markdown support
- 🏷️ Tag filtering and search
- 👥 Contact directory
- 📝 Journal and concept organization
- 🌙 Dark theme UI

## Usage

Open `index.html` in any modern browser:

```
open index.html
```

Or serve locally:

```
python3 -m http.server 8000
# Visit http://localhost:8000
```

## Adding Documents

Edit the `docs` array in `index.html` to add:
- Journal entries (tag with "journal")
- Concept documents
- Research notes

Each document needs:
- `slug`: Unique identifier
- `title`: Display title
- `date`: (optional) Document date
- `tags`: Array of tags
- `content`: Markdown content

## Adding Contacts

Edit the `contacts` array in `index.html` to add:
- `name`: Contact name
- `email`: Email address
- `relationship`: (optional) Relationship or role
- `notes`: (optional) Additional notes
