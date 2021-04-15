# update-updater

The ability to manually update WordPress from the admin area, and to install and update plugins and themes, has existed since 2.3 in 2007.
Auto-update features were added in WordPress 3.7 (for minor releases), extended in 5.5 (as opt-in for plugins and themes), and 5.6 (major releases). To make the user experience of auto-updates even better, and build trust with users and extenders, it’s important that this mechanism works well and provides all the failsafe checks needed.

The WordPress Core update has proven to be generally reliable, but it doesn’t actually have many tests nor is well documented. There are also some reliability concerns around adding new files and the overall number of changed files, which is the reason WordPress currently tries to keep the number of changed files in minor releases to a minimum.

Plugins and themes updaters are older: in general, all of them can be improved.

## Goal
The project goal is to review the existing state of the updaters and propose ways to improve them.

- [WordPress](https://developer.wordpress.org/reference/classes/wp_upgrader/)
- [Core](https://developer.wordpress.org/reference/classes/core_upgrader/)
- [Plugins](https://developer.wordpress.org/reference/classes/plugin_upgrader/)
- [Themes](https://developer.wordpress.org/reference/classes/theme_upgrader/)
- [Update/Install Language Packs](https://developer.wordpress.org/reference/classes/language_pack_upgrader/)
- [Upgrader Skin for WordPress Translation Upgrades](https://developer.wordpress.org/reference/classes/language_pack_upgrader_skin/)

## Outcomes
The expected outcomes are:
1. Making sure the zips upload and unpacking is safe.
2. Create a mechanism to upgrade and roll back.
3. Having managed updates (database migrations).
4. Create a unified JSON convention for requirements and dependencies.

## Safe zip uploads and unpacking
With the introduction of auto-updates, these processes are run even more often. So relatively small issues get triggered more often, and with that become a bigger problem. They also now more often run unattended: an auto-update that breaks could lead to quite problematic results.

The goal here is to address most of the known issues related to downloading and extracting update packages, copying files and directories, improve documentation for updates, add some automated tests, and make the update process more reliable in general.

## Ugrade and rollback
When a core auto-update fails, core has long had the ability to automatically attempt a "rollback" to the latest stable release (in the branch that the site is running). Note: for core auto-updates, "rollback" is not attempted for certain failures (e.g. "disk full", etc).

This capability should be extended to be available for plugin and theme updates.

## Managed updates (data migrations API)

Plugins should be able to easily run database migrations, so that update and rollback could be performed not only for files but also for data.

Yoast already does this by having a migrations library:
https://github.com/Yoast/wordpress-seo/tree/trunk/lib/migrations
https://github.com/Yoast/wordpress-seo/tree/trunk/src/config/migrations

If we had a unified process for data migrations in core, WordPress would be able to run the latest available migration after an update or rollback, without the need to store anything about the previous state. That would not also require anything from the plugin author, apart from adding a "migrations" folder.

## 
Different plugins have introduced compatibility tags (For example, Elementor and WooCommerce). 
In the long run, this could become harder to manage.
This issue could be solved by adding a `requirements.json` file in the root of the plugin or theme. 
