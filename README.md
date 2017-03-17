# Drupal 8 scaffold

## A springboard project for new Drupal 8 projects.

Some areas may be opinionated towards the internal best practices at Real Life Digital, but will stick to community accepted standards as closely as possible.

Provides integration with [platform.sh](https://platform.sh), but isn't dependent on its use. Notably there are some platform.sh sensible default files at:

* .platform.app.yaml
* .platform/routes.yaml
* .platform/services.yaml
* web/sites/default/settings.platformsh.php
* (Include statement in web/sites/default/example.settings.php)

This project differs from the [Drupal 8 project template for Platform.sh](https://github.com/platformsh/platformsh-example-drupal8) in that it uses the [drupal-composer/drupal-scaffold](https://github.com/drupal-composer/drupal-scaffold) to build Drupal's scaffolded files (`index.php`, `.htaccess` etc) required on top of the composer dependencies, rather than including them here in this repo.

This project also aims to provide step-by-step documentation to speed up the roll up time for new projects.

## Improvements

Areas for improvement are welcome through pull requests.

## Prerequisites

* [Composer](https://getcomposer.org/) installed on your development and production environments.
* A working MySQL or MariaDB database already set up with user permissions set.
* You have a remote git repository available and set up to accept your new project's git pushes.
* You have a means of serving the web root from `PROJECT_DIRECTORY`/web wherever you place it on your filesystem.
* MAMP or LAMP stack set up as per [drupal.org system requirements documentation](https://www.drupal.org/docs/7/system-requirements/web-server)

## Get going

**1. Clone this repository and navigate inside.**

```bash
git clone --depth=1 --branch=master git@github.com:reallifedigital/drupal-scaffold.git PROJECT_DIRECTORY
cd PROJECT_DIRECTORY
```

where `PROJECT_DIRECTORY` is the destination directory for the project.

**2. Remove the .git directory so you can make your own git history.**

```bash
rm -rf .git
```

**3. Initialise your repository**

```bash
git init && git config core.filemode false
```

**4. Optionally set your remote repository**

```bash
git remote add origin user@server:repository
```

Alter `user`, `server` and `repository` above to suit your needs.

**5. Create initial commit**

```bash
git add . && git commit -m "Initial commit"
```

**6. Add your remote git repository location**

Note: Ensure permissions are set up on the remote repository (i.e. with your SSH key).

```bash
git remote add origin USER@SERVER:REPO
```

Note: for [platform.sh](https://platform.sh) use:

```bash
git remote add origin PROJECT_ID@git.LOCATION.platform.sh:PROJECT_ID.git
```

Replace PROJECT_ID with the ID seen in the platform.sh UI, and LOCATION with the location which the platform is set up: e.g. 'eu'.

**7. Push master branch to your remote**

```bash
git push origin master
```


**8. Build out the scaffold with the included build script**

```bash
./build
```

Note: this build script can be used in the general development workflow to build new dependencies. See the contents of this file for more information on building with dev dependencies.

**9. Create a settings.php file**

```bash
cp web/sites/default/example.settings.php web/sites/default/settings.php
```

The example file contains sensible defaults which you can alter for the needs of the project.

Any changes you make to settings.php should be for **all** environments and should be checked into your git repository. This file is **not** git-ignored.

**10. Set up you setting.local.php file**

```bash
cp web/sites/default/example.development.settings.local.php web/sites/default/settings.local.php
```

Any changes you make to settings.local.php should be for the current environment only and should **not** be checked into your git repository. This file **is** git-ignored.


Edit the file at `web/sites/default/settings.local.php` and set the `$databases` array with your database settings.

**11. Install Drupal**

Either through the web interface:

`http://SERVER_NAME/install.php`

where `SERVER_NAME` is your remote or local server name where the site is served from - e.g. localhost.

Or use drush:

```bash
drush site-install standard --site-name="New site" --account-name="something_but_not_admin" --account-pass="something_secure" --site-mail="you@yourdomain.tld"
```

Obviously, replace the placeholder argument above with sensible values.

Use: `drush help site-install` for more argument options.

**12. Add your custom code**

* Add your custom theme(s) to web/themes/custom
* Add your custom module(s) to web/modules/custom
* Add your static non-PHP libraries to web/libraries

**13. Install contrib modules and themes with composer**

```bash
composer require drupal/PROJECT_NAME
```

**Tip:** to see available drupal project (module) versions, run:

```bash
composer show -a drupal/PROJECT_NAME | grep versions
```

and then run, for example:

```bash
composer require "drupal/PROJECT_NAME:1.0.0"
```

where `PROJECT_NAME` is the project name at https://drupal.org/project/`PROJECT_NAME`

**13. For any patches to be applied, update composer.json**

First, ensure there is an upstream issue on drupal.org. Add an entry the patches section of the `composer.json` file.

Format to capture key information about the patch should be:

```json
{
    "extra": {
        "patches": {
            "owner/repo": {
                "Module:Version, Issue description, Issue + Comment URL": "https://www.drupal.org/files/issues/example.patch"
            }
        }
    }
}
```

For example:
```json
{
    "extra": {
        "patches": {
            "drupal/address": {
                "Address:8.x-1.x-dev, Add field settings for global overrides of required/optional behavior, https://www.drupal.org/node/2514126#comment-11917633": "https://www.drupal.org/files/issues/2514126-49.field-behavior-settings-as-table.patch"
            }
        }
    }
}
```

* Remember that this is a JSON object - the last patch in the list should not have a trailing comma.
* Remember that composer.json file use 4 spaces for indentation.
* Remember to run `composer install` after updating patch entries.

## Further notes

* Config files located in web/sites/default/files are *not* git-ignored, so are safe to include, however, it's recommended to place the config exports outside the web root in the `../config/` directory. The `example.settings.php` file adds this as the default config directory.
* Uses the [drupal-composer/drupal-scaffold](https://github.com/drupal-composer/drupal-scaffold) project
* .gitignore file handles common use case, but may need to be tweaked to suit your own project
* Once you've run composer you should commit the composer.lock file. This file is not git-ignored.
* `www` symlink is in place for legacy support.

## For contributing to this project

Fork the repo on GitHub and submit pull requests. All feedback is appreciated.

## Further reading:

* [Custom Drupal 8 theme up and running with Sass, Singularity, Breakpoint, LiveReload and Gulp](http://www.reallifedigital.com/blog/how-we-got-custom-drupal-8-theme-and-running-sass-singularity-breakpoint-livereload-and-gulp)
* [Drupal's Coding standards](https://www.drupal.org/docs/develop/standards)

**Author: Barry Fisher**

**Last updated: 2016-03-17**
