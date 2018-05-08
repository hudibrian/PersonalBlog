## What's inside?
*   A WordPress backend that serves its data via the [WP REST API](https://developer.wordpress.org/rest-api/).
*   An automated installer script which bootstraps a core WordPress installation.
*   The WordPress plugins you need to set up custom post types and custom fields ([Advanced Custom Fields Pro](https://www.advancedcustomfields.com/) and [Custom Post Type UI](https://wordpress.org/plugins/custom-post-type-ui/)).
*   Plugins which expose those custom fields and WordPress menus in the [WP REST API](https://developer.wordpress.org/rest-api/) ([ACF to WP API](https://wordpress.org/plugins/acf-to-wp-api/) and [WP-REST-API V2 Menus](https://wordpress.org/plugins/wp-rest-api-v2-menus/)).
*   All the starter WordPress theme code and settings headless requires, including pretty permalinks, CORS `Allow-Origin` headers, and useful logging functions for easy debugging.
*   A mechanism for easily importing data from an existing WordPress installation anywhere on the web using [WP Migrate DB Pro](https://deliciousbrains.com/wp-migrate-db-pro/) and its accompanying plugins (license required).

Let's get started.

## WordPress Backend

Before you install WordPress, make sure you have all the required software installed for your operating system.

### Prerequisites

*   **OS X:** You'll need [Homebrew](https://brew.sh/) and [Yarn](https://yarnpkg.com/en/) installed.
*   **Windows:** To install under Windows you need to be running the _64-bit version of Windows 10 Anniversary Update or later (build 1607+)_. The [Linux Subsystem for Windows](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) should be installed and enabled before proceeding. Then, you'll need the prerequisites for Ubuntu Linux, detailed below, set up.
*   **Ubuntu Linux:** You'll need the latest version of NodeJS, Yarn and debconf-utils installed first. Follow this [simple guide](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions) to get the latest version of NodeJS installed. Install the rest of the packages using the `apt-get` package manager. _Note: During the WordPress installation, you may be asked to enter the root password at the prompt due to the use of the `sudo` command_

### Install

The following command will get WordPress running locally on your machine, along with the WordPress plugins you'll need to create and serve custom data via the WP REST API.

```zsh
> yarn install && yarn start
```

When the installation process completes successfully:

*   The WordPress REST API is available at [http://localhost:8080](http://localhost:8080)
*   The WordPress admin is at [http://localhost:8080/wp-admin/](http://localhost:8080/wp-admin/) default login credentials `nedstark` / `winteriscoming`

### Import Data (Optional)

To import data and media from a live WordPress installation, you can use the Migrate DB Pro plugin, which is already installed. To do so, in the `robo.yml` file, set the plugin license and source install. Run `robo wordpress:setup`, then run `robo wordpress:import` to pull in the data.

### Extend the WordPress API

At this point you can start setting up custom fields in the WordPress admin, and if necessary, creating [custom REST API endpoints](https://developer.wordpress.org/rest-api/extending-the-rest-api/adding-custom-endpoints/) in the Postlight Headless WordPress Starter theme. The primary theme code is located in `wordpress/wp-content/themes/postlight-headless-wp`. As you modify the theme code, be sure to [use WordPress coding standards](https://github.com/postlight/headless-wp-starter/blob/master/wordpress/wp-content/themes/postlight-headless-wp/README.md).

## Troubleshooting Common Errors

**`ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)`**

If you receive this error, it likely means another version of MySQL, not the version that was installed by this script, is being referenced by the MySQL command.

1.  Open up your `.bash_profile`, and see if there is a reference to MySQL in your PATH or if MySQL is being exported as a function. Remove it.

2.  Repeat the installation process. If you still have errors, then look for - and remove - other versions of MySQL by following [these "Remove MySQL" instructions](https://coderwall.com/p/os6woq/uninstall-all-those-broken-versions-of-mysql-and-re-install-it-with-brew-on-mac-mavericks).
