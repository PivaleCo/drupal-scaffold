# Drupal 8 scaffold

## A springboard project for new Drupal 8 projects, using as many standards and best practices as possible.

Some areas may be opinionated towards the internal best practices at Real Life Digital.

Areas for improvement are welcome through pull requests.

## Prerequisites

* [Composer](https://getcomposer.org/) installed on your development and production environments

## Get going

### For general use:

1. Clone this repository.

```bash
git clone --depth=1 --branch=master git://someserver/somerepo PROJECT_DIRECTORY
```

where `PROJECT_DIRECTORY` is the destination directory for the project.

2. Remove the .git directory so you can make your own git history.

```bash
rm -rf !$/.git
```

3. Initialise your repository

```bash
git init
```

4. Optionally set your remote repository

```bash
git remote add origin git://user@server:repository
```

Alter `user`, `server` and `repository` above to suit your needs.

5. Create initial commit

```bash
git commit -a -m "Initial scaffold commit"
```

6. Push master branch to your remote

```bash
git push origin master
```

7. Build out the scaffold with composer

```bash
composer install && composer drupal-scaffold
```

8. 

### For contributing:

Fork the repo on GitHub and submit pull requests!

## Further notes

* .gitignore file handles common use case, but may need to be tweaked to suit your own project



