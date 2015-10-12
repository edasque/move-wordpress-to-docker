# Generic mechanism for moving Wordpress sites to Docker

## Concept

Based on a wordpress site backup (config file, data dump, wp-content directory), a Docker container is created and started. This container also provides a daily backup of the same files.

## Implementation

In the init directory, Docker will find a wp-config file, wp-content directory and SQL dump

> Before copying these files over (and doing a DB dump), all plugins & wordpress itself will have to have been updated to the latest & greatest.

At container creation, once wordpress & dependencies are installed:

1. Database is created
2. MySQL dump is loaded
3. Config file is copied over
4. wp-content directory is copied over
5. instance is brought up

### Naming convention

* config file will be called wp-config.php and found at the root
* Database dump will be called wordpress.sql and found at the root
* Wordpress content directory will be called wp-content and found at the root

## Setup
* something
* another


