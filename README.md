# Openenventory - Full database, webserver and phpmyadmin stack

This is a lamp stack made for the chemical database openenventory.
It includes all needed things and adoptions to run it and can also be deployed behind an already running nginx-proxy.
The code for openenventory has to be downloaded seperately.
***It is not ment to be used at a public network***

## Quick start
* Clone repository
* Change content of example.env according to your needs and rename it to .env
* Download source code of openenventory
	* Put it into the webfolder
	* Do not overwrite lib_global_settings.php if you did not alter NAME_MYSQL in example.env
* Create or reuse a network named according to NAME_NETWORK in example.env with `docker network create NAME_NETWORK`
* run `docker-compose up`
* Open phpMyAdmin, login with root and your password, create a database
* Log in with openenventory in this database


## Configuration of openenventory itself
There is an example config file in the web folder, if you use the example.env, 
you can use the file provided in web/lib_global_settings.php
### File lib_global_settings.php
The database is not running on localhost, so the db_server needs to be changed:
`
define("db_server","oemysql"); //change oemysql to the name you gave to NAME_MYSQL in .env
define("php_server","%"); 	//This allows access to the MYSQL-Server from other hosts
`

## Using openenventory behind a nginx-proxy
You can run openenventory behind a subdomain, even in a local environment without a public DNS record and IP-adress for your server.
We use xip.io for this purpose which gives us back a DNS record containing our local Server-IP and enables to use subdomains.
Means: openenventory.192.168.0.1.xip.io resolves to 192.168.0.1
At your server, the nginxproxy uses the subdomain to forward internally to the openenventory container.
The subdonmain name for openenevtory can be configured in the .env via DOMAIN_OE - it is compatible with the jwilder/nginx-proxy docker-image.

## Advanced stuff:
* You can create the database automatically at the _creation_ of the stack by putting into conf/mysql_dbases/ a corresponding .sql file (see there in the example)

## FAQ:
* Where do if find which port I can reach the webserver/phpMyAdmin?
	* take a look into your .env file
* Why is the naming of the containers done by hand?
	* As this stack is not ment to be massively deployed I found it more convenient to name the containers myself. It further helps me to know what to enter manually in the php-configuration files of open enventory. A automatic naming would be useful if the php-configuration files would be automatically changed, but I did not investigate in that.
* When I deploy a new stack and restore all databases, the users still do not have access to OpenEnventory.
	* This is due to the decicion of OpenEnventory to save users in the mysql-database. A solution is to login in OpenEnventory with root, goto Settings -> Rewrite Users do database


