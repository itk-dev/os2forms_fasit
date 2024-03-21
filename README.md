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

### Certificate

The certificate must be in `pem` or `cer` format and
must be whitelisted by Fasit Schultz.
For this the certificate thumbprint is needed. To get the thumbprint
from the command line run

```sh
openssl x509 -in SOME_CERTIFICATE.pem -noout -fingerprint
```

Example output

```sh
SHA1 Fingerprint=6A:CB:26:1F:39:31:72:D8:7F:A3:99:7C:EC:86:56:97:59:A8:52:8A
```

which should be converted to lowercase and have its colons removed before provided to Fasit Schultz, i.e.

```sh
6acb261f393172d87fa3997cec86569759a8528a
```

## Queue

Archiving is done via an
[Advanced Queue](https://www.drupal.org/project/advancedqueue)
called `fasit_queue`.

The queue should be processed with `drush`:

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
