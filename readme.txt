=== Postnova for MCP ===
Contributors: afatyo
Tags: mcp, ai, automation, content management, publishing, wordpress ai, remote publishing, blog, editorial workflow, abilities api
Requires at least: 6.8
Tested up to: 7.0
Stable tag: 2.2.0
Requires PHP: 7.4
License: MIT
License URI: https://opensource.org/licenses/MIT

Registers safe blog publishing abilities for the WordPress MCP Adapter. AI agents can create, preview, revise, restore, schedule, and manage posts directly.

== Description ==

Postnova for MCP registers 27 blog publishing abilities for use with the WordPress MCP Adapter plugin. AI agents can create, edit, preview, revise, restore, schedule, and manage posts directly without needing WP Admin access.

Postnova includes per-ability controls, object-level permission checks, a content-free activity log, dependency diagnostics, and dry-run previews for safer AI-assisted editing.

Requires the MCP Adapter plugin (WordPress/mcp-adapter). On WordPress 6.9+, the Abilities API is built-in. On 6.8, install the Abilities API plugin separately.

== Installation ==

1. Install and activate the MCP Adapter plugin.
2. Upload postnova-for-mcp.zip via Plugins > Add New > Upload Plugin.
3. Activate the plugin.
4. Configure your MCP client to connect to your WordPress REST API endpoint.

== Changelog ==

= 2.2.0 =
* New: blog/list-revisions — list recent revisions for a post.
* New: blog/get-revision — retrieve the content and metadata of a revision.
* New: blog/restore-revision — safely restore a post to a previous revision.
* New: dry-run previews for blog/update-post, including field and taxonomy changes.
* New: activity log for the latest 100 ability executions without storing post content or raw inputs.
* New: admin diagnostics for the Abilities API, MCP Adapter, and default MCP endpoint.
* Improved: dependency notices and graceful handling when the Abilities API is unavailable.
* Improved: empty tag or category arrays can now intentionally clear the assigned taxonomy.

= 2.1.1 =
* Security: Fixed SSRF vulnerability in blog/upload-media — URL now validated to block internal/private IP ranges and non-HTTP(S) schemes.
* Security: Fixed IDOR vulnerability — all post-level operations (update, get, schedule, duplicate, set-featured-image, delete) now enforce object-level capability checks via current_user_can('edit_post', $id).

= 2.1.0 =
* New: blog/list-media — browse Media Library with optional search and MIME type filter.
* New: blog/delete-media — permanently delete a media attachment by ID.
* New: blog/get-site-info — retrieve site name, URL, timezone, language, and WP version.
* New: blog/get-stats — get post/comment/media counts broken down by status.
* Settings page now shows all 24 abilities.

= 2.0.0 =
* New: Admin settings page (Postnova menu) to enable/disable individual abilities.
* New: Disabled abilities are not registered to MCP at all, as if they don't exist.
* New: Settings stored globally in wp_options under postnova_disabled_abilities.

= 1.6.2 =
* Fix: update-comment no longer errors when status is already the same.
* Tested up to WordPress 7.0.

= 1.6.1 =
* Fix: schedule-post now correctly retains future status instead of publishing immediately.

= 1.6.0 =
* Initial public release with 20 blog post abilities.
