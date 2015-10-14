# Generic mechanism for moving Wordpress sites to Docker

## Concept

Based on a wordpress site backup (~~config file~~, data dump, wp-content directory), a Docker container is created and started. This container also provides a daily backup of the same files.

## Implementation

In the init directory, Docker will find a wp-content directory and SQL dump named wordpress.sql

**Before copying these files over (and doing a DB dump), all themes, plugins & wordpress itself should be up to data (latest WP is mandatory).**

At container creation, once wordpress & dependencies are installed:

1. Database is created
2. MySQL dump is loaded
3. wp-content directory is copied over (then the nginx plugin is installed)
4. instance is brought up

### Naming convention

* config file will be called wp-config.php and found at the root
* Database dump will be called wordpress.sql and found at the root
* Wordpress content directory will be called wp-content and found at the root

### Of note

* the database will be called wordpress, make sure the DB dump doesn't use another database (nor does it create one)
* I'll need help from the community to make this as generic as possible
* The core of this project is a 'fork' from https://github.com/eugeneware/docker-wordpress-nginx

## Usage
Create the image:
```Shell
docker build -t "move-wordpress-to-docker" --no-cache .
```
Examples for creating & running the container:
```Shell
docker run -p 80:80 -v ~/absolute-path-to-the-export-directory/thecloudsaga:/export --name thecloudsaga -d move-wordpress-to-docker
```

Note the mysql password & the WP password in the container log (i.e. write it down)

## TODO
* Do we really need wp-config.php ?
** Doing away with accepting it as input for now
* Can this be supplemental to https://github.com/eugeneware/docker-wordpress-nginx instead of modifying it?
* Rely on exported volumes for wp-content backup
* Create daily backup on exported volume or let people backup by accessing MySQL on 3306
* Figure out how to deploy many of these containers for a multi-host setup (nginx-proxy?)


## Limitations

* If you have a customized wp-config.php file, this application doesn't take that into account

