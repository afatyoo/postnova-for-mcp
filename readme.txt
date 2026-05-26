=== Postnova for MCP ===
Contributors: afatyo
Tags: mcp, claude, ai, blog, automation
Requires at least: 6.8
Tested up to: 7.0
Stable tag: 2.1.0
Requires PHP: 7.4
License: MIT
License URI: https://opensource.org/licenses/MIT

Registers blog post abilities for use with the WordPress MCP Adapter. AI agents like Claude can create, edit, schedule, and manage posts directly.

== Description ==

Postnova for MCP registers blog post abilities for use with the WordPress MCP Adapter plugin. AI agents such as Claude can create, edit, schedule, and manage posts directly without needing WP Admin access.

Requires the MCP Adapter plugin (WordPress/mcp-adapter). On WordPress 6.9+, the Abilities API is built-in. On 6.8, install the Abilities API plugin separately.

== Installation ==

1. Install and activate the MCP Adapter plugin.
2. Upload postnova-for-mcp.zip via Plugins > Add New > Upload Plugin.
3. Activate the plugin.
4. Configure your MCP client to connect to your WordPress REST API endpoint.

== Changelog ==

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
