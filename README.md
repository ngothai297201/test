
This Magento 2.4.6 upgraded from Magento 2.4.7-p1

## Magento System [ Requirements](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements)
* Composer 2.7
* ~Elasticsearch 7.x~
* OpenSearch 2.12
* ~MySQL 8.0~
* MariaDB 10.6
* PHP 8.3
* RabbitMQ 3.12
* Redis 7.2
* Nginx 1.x (1.27.0 the latest mainline version)
* Apache 2.4.x

## Setup database
* Create new table DB
* Import new database form old database (ondemand)

## Upgrade Magento
* Please run there commands:
```
git clone https://github.com/marvelic/ShopOnDemand.git

```
* Note: Delete file composer.lock if it exist before run composer installl
* In command line, using "cd", navigate to your Magento 2 root directory
````
cd ShopOnDemand
git fetch --all
git checkout update_m246
composer install
````
* copy both file config.php and env.php form old ondemand to app/etc
````
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

## Note fix error when remove module dhl/shipping

######This extension is in legacy status since 04/2020 and will run out of maintenance and support after a short transition period. You can find the official replacement extension here https://github.com/netresearch/dhl-shipping-m2. It includes the latest and greatest possible range of functions that DHL is currently offering.

* To clean up the database, run the following commands:

````
DROP TABLE `dhlshipping_quote_address`, `dhlshipping_order_address`;
DROP TABLE `dhlshipping_quote_address_service_selection`, `dhlshipping_order_address_service_selection`;

DELETE FROM `eav_attribute` WHERE `attribute_code` IN ('dhl_dangerous_goods_category', 'dhl_tariff_number', 'dhl_export_description');

ALTER TABLE `quote` DROP COLUMN `dhl_service_charge`, DROP COLUMN `base_dhl_service_charge`;
ALTER TABLE `quote_address` DROP COLUMN `dhl_service_charge`, DROP COLUMN `base_dhl_service_charge`;
ALTER TABLE `sales_order` DROP COLUMN `dhl_service_charge`, DROP COLUMN `base_dhl_service_charge`;
ALTER TABLE `sales_invoice` DROP COLUMN `dhl_service_charge`, DROP COLUMN `base_dhl_service_charge`;
ALTER TABLE `sales_creditmemo` DROP COLUMN `dhl_service_charge`, DROP COLUMN `base_dhl_service_charge`;
DELETE FROM `core_config_data` WHERE `path` LIKE 'carriers/dhlshipping/%';
DELETE FROM `setup_module` WHERE `module` = 'Dhl_Shipping';
````
