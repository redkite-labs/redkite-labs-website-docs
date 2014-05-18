RedKite CMS
===========
Thanks for interesting in the RedKite CMS Application.

A Symfony2 application powered by RedKite CMS with all required vendors installed.

This is the ideal package to have a working application stripped down of all test and 
git folders to minimize the space on the hard disk.

Requirements
------------
1. A web-server like Apache or Nginx
2. Php 5.3.3+
3. A database supported by Propel, like mysql, postgres or sqlite


Download
--------
Download your free `RedKite CMS Application`_ copy now!

Set up RedKite CMS Application
------------------------------
Unpack the RedKite CMS Application into the document root of your web-server.

Web server configuration
~~~~~~~~~~~~~~~~~~~~~~~~
Add a new **VirtualHost** to the web-server to handle the application and configure its
**DocumentRoot** to point the package **web folder**. 

As an alternative to **VirtualHost** you can update the web-server's **DocumentRoot** 
to point the package **web folder**.

.. note::

	Please refer `this guide`_ if you are not comfortable to set up a web-server

Configure the timezone
~~~~~~~~~~~~~~~~~~~~~~
RedKite CMS requires the **date.timezone** parameter configured in the **php.ini** file
for both web server and CLI configurations.

A standard out-of-the-box PHP install comes with that parameter empty on most platforms,
so you must configure it before installing RedKite CMS.

The php.ini file on a *nix machine is usually saved under the **/etc/php5** folder, respectively
under the **apache2** folder, if you use apache as web server, and under the **cli** folder for the
console: you must configure that parameter for both those **php.ini files**.

The configuration is pretty straightforward: just locate the **date.timezone** parameter,
uncomment it removing the semicolon at the begin of that parameter and add your timezone:

.. code-block:: text

    [Date]
    ; Defines the default timezone used by the date functions
    ; http://php.net/date.timezone
    date.timezone = Europe/London

Supported timezones can be found at `http://php.net/manual/en/timezones.php`_.

Xdebug configuration
~~~~~~~~~~~~~~~~~~~~
When you use **Xdebug** with your php installation, you need to configure that module
as follows:

.. code-block:: text
    
    xdebug.max_nesting_level=1000

otherwise you could get an error or, worse, the page rendering could stop, without
displaying nothing on the screen.

.. note::

    If you don't use **Xdebug** you can safety skip this step.

Permissions
~~~~~~~~~~~
Set up the permissions as explained in this `Symfony2 book paragraph`_. This latest step 
is not required for windows users.	

RedKite CMS set up
------------------
RedKite CMS requires several steps to be accomplished to properly set up the CMS itself.
Luckily the **RedKiteCmsInstallerBundle** will do all the job for you. 

This bundle provides a web installer interface or an interactive symfony2 command to 
help you installing RedKite CMS.


Installing from the console
---------------------------
Installing RedKite CMS from the console is really easy:

.. code-block:: text

    app/console redkitecms:configure

This will run the interactive command and provide the required information. If everything works,
you will be prompted that the configuration has been written and you ready to start the install.

.. note::

    By now, you will use the **rkconsole** console instead of the canonical **console** provided
    by Symfony2. The rule is easy: every time you need to run a command for the **rkcms[*]** environments,
    you must use the **rkconsole**

Run the following command from the console:
    
.. code-block:: text

    app/rkconsole redkitecms:install --env=rkcms

.. note::

    Probably you would use a custom bundle instead of the default one: `learn how`_ reading this
    paragraph


Installing using the web interface
----------------------------------
To install RedKite CMS using the web interface, just open a browser and point the following
link:

.. code-block:: text

    http://localhost/install

Provide the required information and you are done! 


Run RedKite CMS
---------------

Open a browser and insert the following url: 

.. code-block:: text

    http://localhost/rkcms.php/backend/login
	
	
Congratulations! 
----------------
Enjoy your RedKite CMS application!!


Use another deploy bundle than the default one
----------------------------------------------
You can use another deploy bundle than the default one provided by RedKite CMS application. This aspect is covered in detail
 in the `Add RedKite CMS to a Symfony2 existing project`_ chapter.

Use another database instead of mysql, postgres or sqlite
---------------------------------------------------------
The **RedKiteCmsInstallerBundle**, which supports you to properly set up RedKite CMS,
can install with one command just the mysql, postgres or sqlite database, but with a
little effort you can easily work with any database supported by Propel, the ORM used
by RedKite CMS to interface with the database.

The first step is to run the following command from  the top folder of your application:

.. code-block:: text

    php app/console redkitecms:configure --no-interaction
	
If you want to use a custom bundle than the default one, use the following command:

.. code-block:: text

    php app/console redkitecms:configure --company=[Your Company] --bundle=[Bundle name] --no-interaction
	
Both these commands write a default mysql database configuration.

Open the **app/config/parameters.yml** file and adapt the following parameters to work
with your database:

.. code-block:: text

    rkcms_database_driver: [YOUR DRIVER]
    rkcms_database_host: localhost
    rkcms_database_port: 3306
    rkcms_database_name: redkite
    rkcms_database_user: root
    rkcms_database_password: null
	
Open the **app/config/rk_cms.yml** and update the **propel** configuration to work with
your database.

.. code-block:: text

    propel:
        [...]

        dbal:
            driver:               %rkcms_database_driver%
            user:                 %rkcms_database_user%
            password:             %rkcms_database_password%
            dsn:                  [YOUR DSN]
            options:              {}
            attributes:           {}

Refer the `Propel official documentation`_ if you require more information about.

When you are done, return to your console and run the following command to complete the installatio:

.. code-block:: text

    php app/rkconsole redkitecms:install --env=rkcms


.. _`RedKite CMS Application` : /download/cms/RedKiteCms-1.1.5.zip
.. _`this guide` : http://symfony.com/doc/current/cookbook/configuration/web_server_configuration.html
.. _`Symfony2 book paragraph` : http://symfony.com/doc/current/book/installation.html#configuration-and-setup
.. _`Propel official documentation` : http://propelorm.org/cookbook/symfony2/working-with-symfony2.html#symfony-configuration
.. _`learn how` : how-to-install-redkite-cms#the-deploy-bundle
.. _`Add RedKite CMS to a Symfony2 existing project` : http://redkite-labs.com/how-to-install-redkite-cms#the-deploy-bundle
.. _`http://php.net/manual/en/timezones.php` : http://php.net/manual/en/timezones.php
