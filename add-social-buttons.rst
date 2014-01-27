How to add the Twitter Share button or the Facebook Like button to your website
===============================================================================

In this article I'll explain in detail how to add the Twitter Share button or the Facebook 
Like button to your website with AlphaLemon CMS. 

In this article I'll refer to the Twitter Share button but the same instructions can 
be applied to the Facebook Like button too.


Install the App-Bundle
----------------------

The very first thing to do is to install the Twitter Share button App-Bundle for
your application.

App-Bundles are always installed by composer, so you must add the App-Bundle package
to the composer.json of your Symfony2 project, which is saved in the top folder of 
the application itself.

Open that file and add the following line to the **require** section:

.. code:: text

    {
        "name": "alphalemon/alphalemon-cms-sandbox",

        [...]

        "require": {

            [...]        

            "alphalemon/app-twitter-share-button-bundle": "dev-master",        
        }
    }

This bundle is not part of packagist repository, in fact it is stored on another repository
at alphalemon.com, so, to fetch it, you must be sure that that repository is declared
into the **repositories** section of your composer.json file:

.. code:: text

    "repositories": [

        ...

        {
            "type": "composer",
            "url": "http://apps.alphalemon.com/"
        }
    ],

.. note::

    If you are using the AlphaLemon CMS sandbox that configuration had been already
    added


To retrieve the package open a terminal console and simply run the following command 
from the top folder of your application:

.. code:: text

    ./php composer.phar update

To complete the installation, you must clear the cache for the **alcms** environment:

.. code:: text

    ./php app/console cache:clear --env=alcms


Define the slot where the button will be placed
-----------------------------------------------
There is any right place where the slot must be added because it depends on how the
website is designed, so I'll report the **alphalemon.com** website experience.

AlphaLemon website has two templates, one for the homepage and one for the internal 
pages, which are the all the other pages than the home. 

Those templates inherit from a base template where are placed the slots repeated for
the whole website's pages.

The best place would have been the base template so the Twitter Share button will be displayed
for the whole website, but my intention was to keep the button very specific for each
argument treated, so I've chosen not to display that button on the homepage but only on
internal pages.

I've added the following code to the **internal** template to add a new slot for the Twitter
Share button:

.. code:: jinja

    <div id="twitter_button">
        {% block twitter_button %}
            {# BEGIN-SLOT
                name: twitter_button
                repeated: site
                htmlContent: |
                    twitter share button
            END-SLOT #}
            {{ renderSlot('twitter_button') }}
        {% endblock %} 
    </div>

The key here is the **site** value for the **repeated** option. This makes the blocks
added to that slot, repeated for all the website's pages, so the **Twitter Share button
will be configured just once for the entire site**.

To have the change applied I've to regenerate the templates so the following command
has been run:

.. code:: text

    ./php app/console alphalemon:generate:templates AlphaLemon2012ThemeBundle


Add the button to the webpage
-----------------------------
At this point, I was ready to add the button to the page, so I've refreshed the page and the new empty
slot has been rendered on the page, ready to receive the block.

I've right clicked on the slot to open the contextual menu and choose the **Twitter Share** button 
from the **add** section.

I've clicked on the block just added to open the editor, which is a form that handles all
the properties exposed by the Twitter Share button.

The most important properties here are the **url** and **title**. 

I have been left both blank in my configuration, because these properties are "page sensitive", 
which means that the tweet will be created using the title of the page and the url of the page.

This is the reason why the slot is repeteable at **site** level for this kind of block: because 
the Twitter Api will create the tweet, fetching the required information from the page
where the block is added.


Change the aspect of the button
-------------------------------
The aspect of the button, when the website with the button has been deployed the first 
time was **horizontal**, then I changed my mind and I decided to display it in **vertical**.

To achieve that job I've edited the button and changed the property **Counter position** 
just once, on a **random page** where and instance of the button exists, and this change 
was applied to all pages due to the repeated status of the slot where the block lives.


Create a specific tweet for each page
-------------------------------------
If you prefer or you need to create a very specific tweet for each page, the slot configuration
must be changed from **site** to **page**.

Obviously in this case each change you want to do must be replicated for each page
of the website.