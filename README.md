# Postnova for MCP

![License](https://img.shields.io/badge/license-MIT-blue)
![WordPress](https://img.shields.io/badge/WordPress-6.8%2B-21759b)
![PHP](https://img.shields.io/badge/PHP-7.4%2B-777bb3)
![Abilities](https://img.shields.io/badge/abilities-24-green)
[![WordPress Plugin](https://img.shields.io/badge/WordPress.org-postnova--for--mcp-blue?logo=wordpress)](https://wordpress.org/plugins/postnova-for-mcp/)

A WordPress plugin that registers blog post *abilities* for use with the [WordPress MCP Adapter](https://github.com/WordPress/mcp-adapter). AI agents like **Claude** can create, edit, schedule, and manage posts directly — no WP Admin needed.

---

## How It Works

```
Claude Code  →  mcp-adapter-execute-ability  →  WordPress REST API  →  Post saved
```

---

## Requirements

| Component | Version |
|---|---|
| WordPress | 6.8+ (7.0+ recommended) |
| PHP | 7.4+ |
| [MCP Adapter](https://github.com/WordPress/mcp-adapter) plugin | Installed & active |
| [Abilities API](https://github.com/WordPress/abilities-api) plugin | Only needed for WP 6.8 |

> On WordPress 6.9+, the Abilities API is built-in — no extra plugin required.

---

## Installation

### Option A: Install from WordPress.org (Recommended)

1. Go to **WP Admin → Plugins → Add New Plugin**
2. Search for **Postnova for MCP**
3. Click **Install Now** → **Activate**

Or install directly from: [wordpress.org/plugins/postnova-for-mcp](https://wordpress.org/plugins/postnova-for-mcp/)

> Make sure the [MCP Adapter](https://wordpress.org/plugins/mcp-adapter/) plugin is also installed and active.

### Option B: Upload ZIP from GitHub Releases

1. Download `postnova-for-mcp.zip` from the [Releases page](https://github.com/afatyoo/postnova-for-mcp/releases/latest)
2. Go to **WP Admin → Plugins → Add New → Upload Plugin**
3. Upload the ZIP → **Install Now** → **Activate**

### Option C: Clone via Git (VPS / SSH)

```bash
cd /var/www/html/wp-content/plugins
git clone https://github.com/afatyoo/postnova-for-mcp.git
```

Activate at **WP Admin → Plugins**.

---

## Settings

After activation, a **Postnova** menu appears in WP Admin sidebar. From there you can:

- See all 24 registered abilities in one table
- Toggle individual abilities on or off with a switch
- Disabled abilities are completely unregistered from MCP — as if they don't exist
- **Enable All** / **Disable All** buttons for quick bulk actions

Settings are global and stored in `wp_options`.

---

## Claude Code Setup

### Step 1 — Create an Application Password in WordPress

1. Go to **WP Admin → Users → Profile**
2. Scroll to **Application Passwords** → enter a name → click **Add New Application Password**
3. **Copy the generated password** — format: `xxxx xxxx xxxx xxxx xxxx xxxx`

### Step 2 — Create `.mcp.json` in your Claude Code project

```json
{
  "mcpServers": {
    "wordpress-blog": {
      "command": "npx",
      "args": ["-y", "@automattic/mcp-wordpress-remote@latest"],
      "env": {
        "WP_API_URL": "https://yourdomain.com/wp-json/mcp/mcp-adapter-default-server",
        "WP_API_USERNAME": "your-wordpress-username",
        "WP_API_PASSWORD": "xxxx xxxx xxxx xxxx xxxx xxxx"
      }
    }
  }
}
```

### Step 3 — Restart Claude Code

> **Important:** Changes to `.mcp.json` require a **full restart** of Claude Code (quit the app, not just `/exit`).

---

## Available Abilities (24)

### Posts

| Ability | Description |
|---|---|
| `blog/create-post` | Create a new post with title, content, status, tags, and categories |
| `blog/update-post` | Update title, content, status, excerpt, tags, and categories of an existing post |
| `blog/get-post` | Get full content and metadata of a post by ID, including tags and categories |
| `blog/list-posts` | List posts with optional filters (status, keyword, count) |
| `blog/delete-post` | Move a post to trash or permanently delete it |
| `blog/schedule-post` | Schedule a post to publish automatically at a future date and time |
| `blog/duplicate-post` | Duplicate a post as a new draft, preserving content, tags, and categories |

### Tags & Categories

| Ability | Description |
|---|---|
| `blog/create-tag` | Create a new post tag |
| `blog/update-tag` | Edit the name, slug, or description of an existing tag |
| `blog/delete-tag` | Permanently delete a tag |
| `blog/list-tags` | List all tags with ID, name, slug, and post count |
| `blog/create-category` | Create a new post category, with optional parent for nested categories |
| `blog/update-category` | Edit the name, slug, description, or parent of an existing category |
| `blog/delete-category` | Permanently delete a category (posts reassigned to default) |
| `blog/list-categories` | List all categories with ID, name, slug, count, and parent |

### Media

| Ability | Description |
|---|---|
| `blog/upload-media` | Upload a media file to the Media Library by fetching from a public URL |
| `blog/set-featured-image` | Set the featured image of a post using a media attachment ID |
| `blog/list-media` | Browse the Media Library with optional search and MIME type filter |
| `blog/delete-media` | Permanently delete a media attachment by ID |

### Comments

| Ability | Description |
|---|---|
| `blog/list-comments` | List comments filtered by post, status, and count |
| `blog/update-comment` | Approve, hold, spam, or trash a comment |
| `blog/reply-comment` | Post a reply to an existing comment as the current user |

### Site

| Ability | Description |
|---|---|
| `blog/get-site-info` | Get site name, URL, timezone, language, and WordPress version |
| `blog/get-stats` | Get post/comment/media counts broken down by status |

---

## Troubleshooting

**MCP not detected after updating `.mcp.json`**
→ Fully quit Claude Code (not just `/exit`), then reopen.

**Abilities not showing up on discover**
→ Verify the MCP Adapter plugin is active. Check that `meta.mcp.public = true` is set on each ability.

**Authentication failed**
→ Use an Application Password, not your regular login password. Format includes spaces: `xxxx xxxx xxxx xxxx xxxx xxxx`.

**Update button not appearing in WP Admin**
→ Go to **Dashboard → Updates → Check Again** to force a refresh. If installed via ZIP (not from WordPress.org), automatic update checks won't work.

---

## License

[MIT License](LICENSE)
