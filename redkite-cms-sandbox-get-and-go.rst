RedKite CMS Get & Go
====================
Thanks for interesting in the RedKite CMS Get & Go Sandbox.

This is a perfect, functioning and portable Symfony2 application powered by RedKite CMS,
ideal to get a quick try to the cms and/or to be used by a single developer.


Requirements
------------
1. A web-server like Apache or Nginx
2. Php 5.3.3+ with the Sqlite extension enabled


Download
--------
Download your free `RedKite CMS Get & Go`_ copy now!


Set up RedKite CMS Sandbox
--------------------------
Unpack the RedKite CMS Sandbox into the document root of your web-server.


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
Set up the permissions as explained in this `Symfony2 book paragraph`_ and
be sure that the application folder has write permissions, otherwise RedKiteCMS
will not be able to save data into the database.

This step is not required for windows users.	


Web site url
~~~~~~~~~~~~
Open the **app/config/config_rkcms.yml** file and change the **http://example.com** website-url
with the url where your application will be deployed:

.. code-block:: text

    red_kite_cms:
        website_url: http://example.com

For example:

.. code-block:: text

    red_kite_cms:
        website_url: http://redkite-labs.com

This setting is required to correctly generate the web site's sitemap.

Run RedKite CMS
---------------
Open a browser and point the following url: 

.. code-block:: text

	http://localhost/rkcms.php/backend/login
	
	
Congratulations! 
----------------
Enjoy your RedKite CMS application!!


.. _`RedKite CMS Get & Go` : /download/cms/RedKiteCms-GetAndGo-1.1.5.zip
.. _`this guide` : http://symfony.com/doc/current/cookbook/configuration/web_server_configuration.html
.. _`Symfony2 book paragraph` : http://symfony.com/doc/current/book/installation.html#configuration-and-setup
.. _`http://php.net/manual/en/timezones.php` : http://php.net/manual/en/timezones.php
