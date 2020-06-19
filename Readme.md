# d8-config

Drupal 8's configuration management experiments.

## Deploy inicial

1\. Clonar o repositório

~~~
$ git clone git@github.com:gedvan/d8-config.git dir
~~~

2\. Instalar as dependências

~~~
$ cd dir
$ composer install
~~~

3\. Criar um banco de dados (MySQL) para o projeto

4\. Carregar o dump inicial

~~~
$ mysql -h [host] -u [user] -p[pass] [dbname] < config/initial-schema.sql
~~~

5\. Criar arquivo de configuração local em `web/sites/default/settings.local.php`
com as informações específicas do ambiente.

~~~
<?php

$databases['default']['default'] = [
  'database' => '',
  'username' => '',
  'password' => '',
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

**Nota:** Para ambiente de desenvolvimento, pode-se utilizar o `web/sites/example.settings.local.php`
como modelo e adicionar as demais configurações no final.

6\. Criar e configurar as permissões da pasta files

~~~
$ mkdir web/sites/default/files
$ chmod a+w web/sites/default/files/
~~~

7\. Importar a configuração

~~~
$ cd web
$ drush cim
~~~
