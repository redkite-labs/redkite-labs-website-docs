RedKite CMS Sandbox without vendors
===================================
Thanks for interesting in the RedKite CMS Sandbox for developers. Hope to get some
pull requests from you sooner!

The same RedKite CMS Sandbox application but requires to install the vendors libraries.

This is the ideal package to start `contributing`_ to RedKite CMS project.

Requirements
------------
1. A web-server like Apache or Nginx
2. Php 5.3.3+
3. A database supported by Propel, like mysql, postgres or sqlite

Download
--------
RedKite CMS Sandbox can be installed using `composer`_. In this case you 
can simply get the latest composer version as follows:

.. code-block:: text

    curl -s http://getcomposer.org/installer | php

or, if you do not have curl installed, you can use:

.. code-block:: text
	
	 php -r "eval('?>'.file_get_contents('https://getcomposer.org/installer'));"

and then run the following command:

.. code-block:: text

    php composer.phar create-project redkite-labs/redkite-cms-sandbox -s stable RedKiteCmsSandbox 1.1.1 --no-dev

This will install a fresh RedKite CMS Sandbox with all the tests and git references.

When composer downloaded all the libraries, follow these `instructions`_ to install your 
RedKite CMS Sandbox.

.. _`composer` : https://getcomposer.org
.. _`contributing` : getting-started-contributing-to-redkite-cms
.. _`instructions` : download-redkite-cms-sandbox#set-up-redkite-cms-sandbox