# OS2Forms GetOrganized

Adds [Fasit Schultz](https://schultz.dk/loesninger/schultz-fasit/) handler for archiving purposes.

## Installation

```sh
composer require os2forms/os2forms_fasit
vendor/bin/drush pm:enable os2forms_fasit
```

## Settings

Configure Fasit API `base url` and a way of getting
certificate on `/admin/os2forms_fasit/settings`.

## Coding standards

Check coding standards:

```sh
docker run --rm --interactive --tty --volume ${PWD}:/app itkdev/php8.1-fpm:latest composer install
docker run --rm --interactive --tty --volume ${PWD}:/app itkdev/php8.1-fpm:latest composer coding-standards-check
```

Apply coding standards:

```shell
docker run --rm --interactive --tty --volume ${PWD}:/app itkdev/php8.1-fpm:latest composer coding-standards-apply
docker run --rm --interactive --tty --volume ${PWD}:/app node:18 yarn --cwd /app coding-standards-apply
```
