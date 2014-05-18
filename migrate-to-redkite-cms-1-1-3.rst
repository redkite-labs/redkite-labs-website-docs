
Upgrade to RedKite CMS
======================

This document explains how to migrate from **RedKite CMS 1.1.2** to **1.1.4** release.

.. note::

    If your application is at **1.1.3** release, you can safely skip this one and refer `this migration document`_ .

There are two possibilities to upgrade your application:

1. From composer
2. Copying RedKite CMS bundles into the src folder of your application (suggested)

Whether or not the method you will choose, you will need to download the `upgrade package`_ and unzip it into the src
folder of your application.

Upgrading from composer
-----------------------

Follows these steps to upgrade from composer:

1. Be sure you composer.json requires the right RedKite CMS packages version:

.. code-block:: text

    "require": {
        [...]
        "redkite-cms/redkite-cms-bundle": "1.1.*",
        "redkite-cms/installer-bundle": "1.1.*",
        "redkite-labs/modern-business-theme-bundle": "1.1.*",
    	"redkite-labs/bootbusiness-theme-bundle": "1.1.*",
        "redkite-cms/redkite-cms-base-blocks": "1.1.*",
        "redkite-cms/tinymce-block-bundle": "1.1.*"
    },

then run

.. code-block:: text

    php composer.phar update

2. RedKite CMS is highly decoupled from your Symfony2 application and, since 1.1.3 release, it lies on its own kernel.
For that reason the **BootbusinessBUndle** has been removed from the AppKernel and moved to the new kernel. Read
`this document`_ to learn more about this topic. If you prefer to continue autoloading your themes in the production
environment, you can safety skip this step.

Open the app/AppKernel.php file and remove the following code:

from **registerBundles** method:

.. code-block:: php

    new RedKiteLabs\BootstrapBundle\RedKiteLabsBootstrapBundle(),

    $bootstrapper = new \RedKiteLabs\BootstrapBundle\Core\Autoloader\BundlesAutoloader(__DIR__, $this->getEnvironment(), $bundles);
    $bundles = $bootstrapper->getBundles();

and from **registerContainerConfiguration** method:

.. code-block:: php

    $configFolder = __DIR__ . '/config/bundles/config/' . $this->getEnvironment();
    if (is_dir($configFolder)) {
       $finder = new \Symfony\Component\Finder\Finder();
       $configFiles = $finder->depth(0)->name('*.yml')->in($configFolder);
       foreach ($configFiles as $config) {
           $loader->load((string)$config);
       };
    }

then replace this last one with the Symfony2 default:

.. code-block:: php

    public function registerContainerConfiguration(LoaderInterface $loader)
    {
        $loader->load(__DIR__.'/config/config_'.$this->getEnvironment().'.yml');
    }

Add the following code to **registerBundles** method:

.. code-block:: php

    // RedKiteCms Active Theme
    $bundles[] = new RedKiteLabs\ThemeEngineBundle\RedKiteLabsThemeEngineBundle();
    $bundles[] = new RedKiteCms\Theme\ModernBusinessThemeBundle\ModernBusinessThemeBundle();
    // End RedKiteCms Active Theme

If you don't use the **ModernBusinessThemeBundle**, replace that bundle entry with the active theme
you are using in your website.


.. note::

    Feel free to add those bundles to **$bundles** array but that configuration might be mandatory
    when the new version will be released.

3. Remove the cache folder and run

.. code-block:: text

    php app/console

to check that everything works again for your production environment.

4. Run the following commands to complete the migration:

.. code-block:: text

    php app/rkconsole propel:model:build --env=rkcms
    php app/rkconsole assets:install web --env=rkcms [--symlink]
    php app/rkconsole assetic:dump --env=rkcms
    php app/rkconsole propel:model:build --env=rkcms
    php app/rkconsole ca:c --env=rkcms[_dev]

Please notice that RedKite CMS commands, the ones for the **rkcms[dev]** environment[s] are
now run by the **rkconsole** instead of the standard **console**, this because RedKite CMS
uses a new Kernel instead of the Symfony2 one, to keep things separated.


Upgrade by copying RedKite CMS bundles into the src folder of your application
------------------------------------------------------------------------------

Follows these steps to upgrade by copying RedKite CMS bundles into the src folder of your 
application:

1. Remove these entries from your composer.json

.. code-block:: text

    "require": {
        [...]
        "redkite-cms/redkite-cms-bundle": "dev-master",
        "redkite-cms/installer-bundle": "dev-master",
    	"redkite-labs/bootbusiness-theme-bundle": "dev-master",
        "redkite-cms/redkite-cms-base-blocks": "dev-master",
	    "redkite-cms/tinymce-block-bundle": "dev-master"
    },

add these entries:

.. code-block:: text

    "require": {
        [...]
        "propel/propel-bundle": "1.2.*",
        "propel/propel1": "1.7.0",
        "knplabs/knp-markdown-bundle": "1.2.*@dev"
    },

then run

.. code-block:: text

    php composer.phar update

Now follow from the step 2 of the other procedure.


Upgrade the dependencies
------------------------

Maybe some of your classes inherit from RedKite CMS core objects, so you need to upgrade those dependencies because since
**RedKite CMS 1.1.2** the prefix **Al** has been removed from the whole core library.


.. _`upgrade package` : http://redkite-labs.com/download/cms/redkite-cms-1-1-4-upgrade.zip
.. _`this migration document` : https://github.com/redkite-labs/RedKiteCms/blob/master/MIGRATE-REDKITE-CMS-1.1.4.md
.. _`upgrade package` : http://redkite-labs.com/download/cms/redkite-cms-1-1-4-upgrade.zip

