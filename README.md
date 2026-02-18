# Goodreads Skill for Openclaw

An Openclaw skill that lets AI agents interact with [Goodreads](https://www.goodreads.com) through browser automation. Since the Goodreads API was deprecated in 2020, this skill uses the `browser` tool to navigate and interact with Goodreads pages directly.

## Features

1. **Search for Books** — Find books by title, author, ISBN, or keyword
2. **Get Book Details & Reviews** — Retrieve title, author, rating, description, and top reviews for any book
3. **Get Personalized Recommendations** — Access your Goodreads recommendations (requires login)
4. **Manage Reading Lists** — Add books to shelves, mark as read, and rate books (requires login)

## Authentication

Some features require an active Goodreads login session in the browser:

| Feature | Login Required |
|---------|---------------|
| Search for books | No |
| View book details & reviews | No |
| Get recommendations | Yes |
| Manage reading lists | Yes |

When a login is needed, the skill will detect the auth state and prompt you. If you are prompted that you are not logged in, there should be an open window of the browser with the Goodreads page already open — please log in to Goodreads in that browser window before continuing.

## Installation

### Via Clawhub (recommended)

```bash
clawhub install goodreads
```

### Manual Installation

Clone this repository into your Openclaw skills directory:

```bash
git clone https://github.com/surajssd/openclaw-goodreads-skill.git ~/.openclaw/skills/goodreads
```

Or symlink from a local clone:

```bash
mkdir -p ~/.openclaw/skills
ln -s "$(pwd)/goodreads" ~/.openclaw/skills/goodreads
```

### Verify Installation

```bash
openclaw skills list            # Should show "goodreads" in the list
openclaw skills info goodreads  # Show skill details
openclaw skills check           # Validate skill structure
```

## Browser Setup

This skill requires a browser configured in Openclaw. We recommend [Brave Browser](https://brave.com).

### 1. Install Brave Browser

Download and install Brave from [brave.com/download](https://brave.com/download).

### 2. Configure Openclaw

Add the browser configuration to `~/.openclaw/openclaw.json`:

**macOS:**

```json
{
  "browser": {
    "executablePath": "/Applications/Brave Browser.app/Contents/MacOS/Brave Browser",
    "defaultProfile": "openclaw"
  }
}
```

**Linux:**

```json
{
  "browser": {
    "executablePath": "/usr/bin/brave-browser",
    "defaultProfile": "openclaw"
  }
}
```

For more details on browser configuration, see the [Openclaw Browser Tool documentation](https://docs.openclaw.ai/tools/browser).

## Usage

Invoke the skill in any Openclaw chat session:

```
/goodreads search for dune
/goodreads tell me about project hail mary by andy weir
/goodreads what are my recommendations?
/goodreads add the midnight library to my want to read shelf
```

Or use the generic skill invocation:

```
/skill goodreads search for the name of the wind
```

## How It Works

The skill instructs the AI agent to use the `browser` tool to:

1. Navigate to the appropriate Goodreads page
2. Take a snapshot of the page content
3. Extract relevant information from the snapshot
4. Interact with page elements (click buttons, fill forms) as needed

All interactions happen through real browser automation — no API calls are made.

## Project Structure

```
goodreads/
├── SKILL.md                # Main skill definition
├── references/
│   ├── URLS.md             # Goodreads URL patterns
│   ├── SELECTORS.md        # Page structure hints
│   └── WORKFLOWS.md        # Browser interaction sequences
└── assets/
    └── error-handling.md   # Error scenarios & recovery
```

## Contributing

Since Goodreads can change its page structure at any time, contributions to keep selectors and workflows up to date are welcome. When submitting changes:

1. Test all four skill capabilities (search, details, recommendations, shelves)
2. Test both logged-in and logged-out scenarios
3. Update `references/SELECTORS.md` if page structure changed
4. Update `references/WORKFLOWS.md` if interaction flows changed

## Disclaimer

This project is not affiliated with, endorsed by, or sponsored by Goodreads or Amazon. Goodreads is a trademark of Amazon.com, Inc. or its affiliates. This skill interacts with the publicly accessible Goodreads website through browser automation.

## License

MIT
