RedKite CMS Sandbox
===================
Here you will learn how to upgrade your RedKite CMS Sandbox with vendors. 

Please notice that this upgrade only works for standard RedKite CMS Sandboxes, this
means that if you are using other packages, you need to upgrade your application using
composer as well.

Download
--------
Download your free `RedKite CMS Sandbox upgrade`_ now!

Install
-------
1. Backup the application's vendor folder, giving it another name, for example **vendor_beta**.
2. Unpack the package into the top folder of your application.
3. Open the README file, when present, and proceed with the instructions you will find inside.
4. Run the following commands:

.. code:: text

    php app/console assets:install --env=rkcms web [--symlink]
    php app/console assetic:dump --env=rkcms
    php app/console ca:c --env=rkcms

.. _`RedKite CMS Sandbox upgrade` : /download/cms/RedKiteCmsSandbox-1.1.1-upgrade.zip