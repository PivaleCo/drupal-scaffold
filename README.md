# Drupal 8 scaffold

## A springboard project for new Drupal 8 projects, using as many standards and best practices as possible.

Some areas may be opinionated towards the internal best practices at Real Life Digital.

Areas for improvement are welcome through pull requests.

## Prerequisites

* [Composer](https://getcomposer.org/) installed on your development and production environments
* A working MySQL or MariaDB database already set up with user permissions set.
* You have a remote git repository available and set up to accept your git pushes.

## Get going

**1. Clone this repository.**

```bash
git clone --depth=1 --branch=master git@github.com:reallifedigital/drupal-scaffold.git PROJECT_DIRECTORY
```

where `PROJECT_DIRECTORY` is the destination directory for the project.

**2. Remove the .git directory so you can make your own git history.**

```bash
rm -rf !$/.git
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
git commit -a -m "Initial scaffold commit"
```

**6. Push master branch to your remote**

```bash
git push origin master
```

**7. Build out the scaffold with composer**

```bash
composer install && composer drupal-scaffold
```

**8. Create a settings.php file**

```bash
cp web/sites/default/example.settings.php web/sites/default/settings.php
```

The example file contains sensible defaults which you can alter for the needs of the project.

Any changes you make to settings.php should be for **all** environments and should be checked into your git repository. This file is **not** git-ignored.

**9. Set up you setting.local.php file**

```bash
cp web/sites/default/example.development.settings.local.php web/sites/default/settings.local.php
```

Any changes you make to settings.local.php should be for the current environment only and should **not** be checked into your git repository. This file **is** git-ignored.


Edit the file at `web/sites/default/settings.local.php` and set the `$databases` array with your database settings.

**10. Install Drupal**

Either through the web interface:

`http://SERVER_NAME/install.php`

where `SERVER_NAME` is your remote or local server name where the site is served from - e.g. localhost.

Or use drush:

```bash
drush site-install standard --site-name="New site" --account-name="something_but_not_admin" --account-pass="something_secure" --site-mail="you@yourdomain.tld"
```

Obviously, replace the placeholder argument above with sensible values.

Use: `drush help site-install` for more argument options.

**11. Add your custom code**

* Add your custom theme(s) to web/themes/custom
* Add your custom module(s) to web/modules/custom
* Add your static non-PHP libraries to web/libraries

## For contributing

Fork the repo on GitHub and submit pull requests!

## Further notes

* Config files located in web/sites/default/files are *not* git-ignored, so are safe to include
* Uses the [drupal-composer/drupal-scaffold](https://github.com/drupal-composer/drupal-scaffold) project
* .gitignore file handles common use case, but may need to be tweaked to suit your own project
* Once you've run composer you should commit the composer.lock file. This file is not git-ignored.

**Author: Barry Fisher**

**Last updated: 2016-02-08**