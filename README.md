# DrupalSecurity

DrupalSecurity is a library for automated Drupal code security reviews. It
defines rules for [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)

Note that Javascript has not been supported yet. To check and fix Javascript files
please use [ESLint](http://eslint.org/) and see the
[Drupal ESLint](https://www.drupal.org/node/1955232) documentation.

## Global installation

First, install composer if you haven't already:

```shell
brew install composer
```

Then install with composer PHP_Codesniffer, PHPCSUtils, and Drupal Coder:

```shell 
composer global require --dev drupal/coder 
composer global require --dev phpcsstandards/phpcsutils
```

Next, make the `phpcs` command globally available. Assuming you are running zsh:

```shell
echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.zshrc
zsh # Reload shell so phpcs is immediately available
```

Clone this repository to a location of your choice. Once you have done this, save the path to a variable:

```shell
DS_PATH=/path/to/DrupalSecurity
```

Then add this repository to PHPCS's set of available standards:

```shell
ORIG_PATHS=$(phpcs --config-show | sed -n 's/^installed_paths: //p')
phpcs --config-set installed_paths ${ORIG_PATHS},${DS_PATH}
```

If it is installed correctly, `DrupalSecurity` should appear in the list of standards when running `phpcs -i`.

## Usage

Check Drupal Security standards

    phpcs --standard=DrupalSecurity --extensions=php,module,inc,install,theme,yml,twig /path/to/drupal/module
