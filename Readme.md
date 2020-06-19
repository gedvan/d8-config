# d8-config

Drupal 8's configuration management experiments.

## Dependencies

- Apache 2+
- PHP 7.3+
- Mysql 5+
- Composer (https://getcomposer.org/)
- Drush launcher (https://github.com/drush-ops/drush-launcher)

## Setup localhost

1\. Clone the repository

~~~
$ git clone git@github.com:gedvan/d8-config.git dir
~~~

2\. Install Composer dependencies

~~~
$ cd dir
$ composer install
~~~

3\. Create a MySQL database

4\. Load the initial database dump

~~~
$ mysql -u [dbuser] -p[dbpass] [dbname] < config/initdb.sql
~~~

5\. Create local settings file at `web/sites/default/settings.local.php`

The minimum settings are:

~~~
<?php

$databases['default']['default'] = [
  'database' => '[dbname]',
  'username' => '[dbuser]',
  'password' => '[dbpass]',
  'prefix' => '',
  'host' => 'localhost',
  'port' => '3306',
  'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql',
  'driver' => 'mysql',
];

$settings['trusted_host_patterns'] = [
  '^localhost$'
];
~~~

To enable development settings, you may copy `web/sites/example.settings.local.php` and change db info.

6\. Create and setup permissions for files folder

~~~
$ mkdir web/sites/default/files
$ chmod a+w web/sites/default/files/
~~~

7\. Import current configuration

~~~
$ drush cim
~~~

8\. Setup web server (alias, virtualhost, etc.)

## Development workflow

### Start a development cycle

1\. Get the latest code from repository

~~~
$ git pull
~~~

2\. Install Composer dependencies

~~~
$ composer install
~~~

3\. Run database updates

~~~
$ drush updb
~~~

4\. Clean cache and import configuration

~~~
$ drush cr
$ drush cim
~~~

### Pushing your work

1\. Export your configuration changes

~~~
$ drush cex
~~~

2\. Commit and push

~~~
$ git add .
$ git commit -m "Commit message"
$ git push [remote] [branch]
~~~

## Important folders

- `config/sync`: where the site configuration is imported from/exported to
- `vendor`: where Composer downloads non-Drupal specific packages
- `web`: Drupal root (must be the web server document root)
- `web/core`: Drupal core
- `web/modules/contrib`: where Composer downloads Drupal modules
- `web/modules/custom`: where custom modules should be created
- `web/themes/contrib`: where Composer downloads Drupal themes
- `web/themes/custom`: where custom themes should be created
- `web/libraries`: where external libraries should be placed
- `web/sites/default/files`: Drupal's public files folder
