OroPlatform Application
=======================

What is OroPlatform?
--------------------

OroPlatform is a business application process management system that is a backbone of the OroCRM and OroCommerce.

OroCommerce is an open-source Business to Business Commerce application built with flexibility in mind. It can be customized and extended to fit any B2B commerce needs.
You can find out more about OroCommerce at [www.orocommerce.com](https://www.orocommerce.com/).

OroCRM is an open-source customer relationship Management application built with flexibility in mind. It can be customized and extended to fit any business needs.
You can find out more about OroCRM at [www.orocrm.com](https://www.orocrm.com/).

This OroPlatform application is an example of a fully functional application created with [OroPlatform](https://github.com/oroinc/platform). It can be used as a blueprint for custom business application development.

System Requirements
-------------------

Please see the OroCRM online documentation for the complete list of [system requirements](https://doc.oroinc.com/backend/setup/system-requirements/).

Installation
------------

Please see the online [OroCRM Installation Guide](https://doc.oroinc.com/backend/setup/dev-environment/manual-installation/crm-ce/) for the detailed installation steps.

Resources
---------

  * [OroPlatform Documentation](https://doc.oroinc.com)
  * [Contributing](https://doc.oroinc.com/community/contribute/)
  
Installation which WARP by SummaSolutions
-----------------------------------------
Start Warp Engine
```sh
warp init
```

Send files to container
```sh
#Only in MacOs
warp sync push --all
```

Install Dependencies 
```sh
warp composer install

#Some parameters are missing. Please provide them.
#database_driver (pdo_mysql): pdo_pgsql
#database_host (127.0.0.1): postgres
#database_port (null): 5432
#database_name (b2b_crm_dev): warp_db
#database_user (root): warp
#database_password (null): Warp2020
#database_driver_options ({  }):
#mailer_transport (mail): smtp
#mailer_host (127.0.0.1): mailhog
#mailer_port (null): 1025
```
Update NodeJs and install pdo_psql unsupported warp php-7.3

``` bash
warp php ssh --root

#Remove node 11.x
apt-get purge nodejs
rm -r  /etc/apt/sources.list.d/nodesource.list

#Download node 12.x
curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh
chmod +x nodesource_setup.sh
./nodesource_setup.sh

# Install node 12.x 
apt-get install -y nodejs build-essential

# Install pdo_psql
apt-get update && apt-get install -y libpq-dev \ && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \ && docker-php-ext-install pdo pgsql pdo_pgsql \ && docker-php-ext-enable pdo pgsql pdo_pgsql

```

Install Oro App
``` bash
warp php ssh

bin/console oro:install \
--application-url="oro-platform41.local" \
--env="prod" --user-name="admin" \ 
--user-email="admin@summasolutions.net" \
--user-firstname="Summa" \
--user-lastname="Solutions" \
--user-password="SummaAdmin" \
--sample-data="y" \
--organization-name="Summa Solutions" \
--language="en" \
--formatting-code="en" \
--timeout=10000
```

Add to Host 
``` bash
# /etc/hosts
127.0.0.1  oro-platform41.local
``` 

Send files from container to host
```sh
#Only in MacOs
warp sync pull --all
```

License
-------

[MIT][1] Copyright (c) 2013 - 2017, Oro, Inc.

[1]:    LICENSE
