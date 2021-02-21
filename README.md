# wessla
Run Laravel 7+ in Windows WSL2 with separate HTTP and PHP containers.

## Quickstart
Make sure you have Docker installed and that you have checked "Use the WSL2 based engine".

Install or create a new Laravel project on your WSL2 drive (the network mount).

Install wessla as a composer dependency:
```
composer require johanfrank/wessla --dev
```
Reload your shell.

Replace your docker-compose calls (or update aliases with new) calls using wessla:

| Description        | Command                    |
| ------------------ | ---------------------------|
| Starting & stopping containers:                 |
| - Build            | `wessla build`             |
| - Up               | `wessla up`                |
| - Down             | `wessla down`              |
| Working from the shell:                         |
| - Artisan            | `wessla artisan {args}`  |
| - Artisan Tinker     | `wessla tinker`          |
| - Composer           | `wessla composer {args}` |
| - PHPUnit            | `wessla test {args}`     |
| Misc:                                           |
| - Bash (interactive) | `wessla bash`            |
| - PHP                | `wessla php {args}`      |


## Why
Since Laravel 8 we have had the option to use Laravel Sail as a wrapper around Docker Compose, which works well for
local development. But unfortunately Sails is built around a rather large "app container" with PHP, HTTP and Supervisor
(for workers). For those who want to mirror their production environment with PHP and HTTP server (Nginx) in isolated
containers, building "dev images" upon the same base that their production environment uses, this becomes messy.

## What Wessla does
* Based on Laravel Sails, Wessla assumes a working set of containers assuming an app built on:
    * A HTTP container,
    * A PHP container,
    * A database (as a container or separate managed instance in production).
* In order to get this working in WSL2, some configuration of users and groups is required
when building your local app (since Docker runs as root:root).
* See `example-app/` for a suggested starting point building isolated containers that should
work locally for quickly getting up and running.

## Known issues & bugs
* Could not get Nginx to run as the correct user, so in order to log errors to `storage/logs/laravel.log` you need to
  make that writable using `chmod 777`.