This Magento 2.3.5

## Magento System [ Requirements](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements)
* Currenty Composer 2.3.0 (suggest composer <= 2.2)
* PHP 7.1


## Clone  Magento
* Please run there commands:
```
git clone https://github.com/datwiki/dulcefina

````

* copy both file config.php and env.php form old ondemand to app/etc

run CLI
 + php bin/magento setup:upgrade
 + php bin/magento setup:di:compile
 + php bin/magento setup:static-content:deploy -f 
 + php bin/magento cache:flush
 + php bin/magento cache:clean config

````
````
* copy file pub/media form old ondemand to pub/media
````

## Note fix error when add module Shippo and Warehouse Email


* composer required library support Shippo and Warehouse Email:
* Currently run composer 2.3.0 , so not install :

````
composer self-update --1
composer require dompdf/dompdf shippo/shippo-php
````
