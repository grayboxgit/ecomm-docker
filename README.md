# eComm Docker Images

## m2-apache
My m2-apache container is built on `fballiano/magento2-apache-php` and exists solely to version-lock that image via my own tags.

### Version 1.3.2
* **Apache:** 2.4.38
* **PHP:** 7.4.19
* **Xdebug:** 2.9.6

### Example `docker-compose.yml` commands:

```
command: >
  sh -c '
    cd /var/www/html/
    sudo chown -R www-data /var/www/.composer;
    sudo -u www-data php -d memory_limit=-1 `which composer` install
    sudo rm -Rf /var/www/html/generated/code/*; sudo chown -R www-data generated
    chown -R www-data pub/static; chown -R www-data generated; chown -R www-data var; chown -R www-data vendor;
    sudo -u www-data php bin/magento cache:enable config layout block_html collections reflection db_ddl compiled_config eav customer_notification config_integration config_integration_api target_rule config_webservice translate vertex
    sudo -u www-data php bin/magento setup:upgrade
    sudo -u www-data php bin/magento setup:di:compile
    sudo -u www-data php bin/magento app:config:import
    sudo -u www-data php bin/magento c:f
    /start.sh
  '
```

## m2-apache-grunt
Similar to `m2-apache` above, `m2-apache-grunt` exists to version-lock the `fballiano/magento2-apache-php` image it is based on. However, I've also installed Grunt to compile Magento's themes. This was installed on top of Apache because Magento 2's Grunt implementation requires PHP.

### Version 1.0.1
* **Apache:** 2.4.38
* **PHP:** 7.3.206
* **NodeJS:** 11.14.0
* **NPM:** 6.7.0

### Example `docker-compose.yml` commands:

```
command: >
  sh -c '
    cd /var/www/html/
    npm install
    npm update
    grunt exec
    chown -R www-data pub/static; chown -R www-data generated; chown -R www-data var; chown -R www-data vendor
    grunt less
    grunt watch
  '
```