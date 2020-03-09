# Magento2 Moudle Creation

# To create Hello World module in Magento 2.
_**For Best Use PHP Storm**_
### To create Hello World module, you need to complete the following high-level steps:
_**Best Practice Use PHP Storm**_

Step 1: Create the folder of Hello World module

Step 2: Create module

Step 3:  Register the Created Module

Step 4: Enable the module

### Step 1: Create Folder of HelloWorld
 Name of the module is defined as “VendorName_ModuleName”. First part is name of the vendor and last part is name of the module: For example: Sathya_HelloWorld.

 ##### _create file directory as_
 ```Shell
 Magento2/app/code/Sathya/HelloWorld
```
### Step 2: Create Module
##### _it is necessary to create etc folder and add the module.xml file_
 ```Shell
 app/code/Sathya/HelloWorld/etc/module.xml
 ```
Contents would be:

 ```Shell
 <?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Sathya_HelloWorld" setup_version="1.0.0">
    </module>
</config>
```
### Step 3 : Register the Created Module
_Create Registration.php file_
```Shell
 app/code/Sathya/HelloWorld/registration.php
```
Contents would be:

```php
<?php
\Magento\Framework\Component\ComponentRegistrar::register(
	\Magento\Framework\Component\ComponentRegistrar::MODULE,
	'Sathya_HelloWorld',
	__DIR__
);
```

### Step 4: Enable the module

Before enable the Module make sure whether the Module is created or not. For that run the command from the Magento root directory as.
```Shell
 php bin/magento module:status
```
It Lists all the Disabled Modules

 ######  Sathya_HelloWorld

To enable the Module run the command as:

```Shell
 php bin/magento module:enable Sathya_HelloWorld
```
###### Also there is an another way to enable it. Which will be  explained later.


Please upgrade your database: Run “bin/magento setup:upgrade” from the Magento root directory.

Let run the command:
```Shell
  php bin/magento setup:upgrade
```
Please run

```Shell
  php bin/magento setup:static-content:deploy
```

Then run **(optional)**
```Shell
  php bin/magento setup:static-content:deploy -f
```

To add route, it is necessary to create **_routes.xml_** file
```shell
app/code/Sathya/HelloWorld/etc/frontend/routes.xml
```

Content would be:
```PHP
<?xml version="1.0" ?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route frontName="helloworld" id="helloworld">
            <module name="Sathya_HelloWorld"/>
        </route>
    </router>
</config>
```
The directory and file you need to create is:
```Shell
app/code/Sathya/HelloWorld/Controller/Index/Test.php
```
Contents would be:
```PHP
<?php
namespace Sathya\HelloWorld\Controller\Index;

class Test extends \Magento\Framework\App\Action\Action
{
	protected $_pageFactory;

	public function __construct(
		\Magento\Framework\App\Action\Context $context,
		\Magento\Framework\View\Result\PageFactory $pageFactory)
	{
		$this->_pageFactory = $pageFactory;
		return parent::__construct($context);
	}

	public function execute()
	{
		echo "Hello World";
		exit;
	}
}
```
After completed, please run command  to clear cache
```Shell
php bin/magento c:f
```
Check your Module by entering  URL now should be as:
```Shell
 http://< YourDomain.com >/helloworld/index/test
 ```
 
