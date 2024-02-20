# OS2Forms Fasit

Adds [Fasit Schultz](https://schultz.dk/loesninger/schultz-fasit/)
handler for archiving purposes.

## Installation

```sh
composer require os2forms/os2forms_fasit
vendor/bin/drush pm:enable os2forms_fasit
```

## Settings

Configure Fasit API `base url` and a way of getting
certificate on `/admin/os2forms_fasit/settings`.

## Queue

Archiving is done via an
[AdvanedQueue](https://www.drupal.org/project/advancedqueue)
called `fasit_queue`.

The queue should be processed via `drush`.

```sh
drush advancedqueue:queue:process fasit_queue
```

List the queue (and all other queues) with

```sh
drush advancedqueue:queue:list
```

or go to `/admin/config/system/queues/jobs/fasit_queue`
for a graphical overview of jobs in the queue.

### Cronjob

Consider running the queue via a cronjob.

```cron
*/5 * * * * /path/to/drush advancedqueue:queue:process fasit_queue
```

## Coding standards

Check coding standards:

```sh
// PHP CS Fixer
docker run --rm --interactive --tty --volume ${PWD}:/app itkdev/php8.1-fpm:latest composer install
docker run --rm --interactive --tty --volume ${PWD}:/app itkdev/php8.1-fpm:latest composer coding-standards-check

// Markdownlint
docker run --rm --interactive --tty --volume ${PWD}:/app node:20 yarn --cwd /app install
docker run --rm --interactive --tty --volume ${PWD}:/app node:20 yarn --cwd /app coding-standards-check
```

Apply coding standards:

```shell
docker run --rm --interactive --tty --volume ${PWD}:/app itkdev/php8.1-fpm:latest composer coding-standards-apply
docker run --rm --interactive --tty --volume ${PWD}:/app node:20 yarn --cwd /app coding-standards-apply
```
