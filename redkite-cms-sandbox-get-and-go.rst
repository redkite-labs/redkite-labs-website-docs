Get & Go Sandbox
================
Thanks for interesting in the Get & Go RedKite CMS Sandbox.

This is a perfect, functioning and portable Symfony2 application powered by RedKite CMS,
ideal to get a quick try to the cms and/or to be used by a single developer.


Requirements
------------
1. A web-server like Apache or Nginx
2. Php 5.3.3+ with the Sqlite extension enabled


Download
--------
Download your free `Get & Go Sandbox`_ copy now!


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

Xdebug configuration
--------------------
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


Web site url
~~~~~~~~~~~~
Open the **app/config/config_rkcms.yml** file and change the **http://example.com** website-url 
with the url where your application will be deployed:

.. code-block:: text

    red_kite_cms:
        website-url: http://example.com

For example:

.. code-block:: text

    red_kite_cms:
        website-url: http://redkite-labs.com

This setting is required to correctly generate the web site's sitemap.

Run RedKite CMS
---------------
Open a browser and point the following url: 

.. code-block:: text

	http://localhost/rkcms.php/backend/login
	
	
Congratulations! 
----------------
Enjoy your RedKite CMS application!!


.. _`Get & Go Sandbox` : /download/cms/RedKiteCmsSandbox-GetAndGo-1.1.1.zip
.. _`this guide` : http://symfony.com/doc/current/cookbook/configuration/web_server_configuration.html
.. _`Symfony2 book paragraph` : http://symfony.com/doc/current/book/installation.html#configuration-and-setup