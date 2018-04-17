.. center::
Basic File Structure

.. div:: row
 .. div:: col-sm-6
  **Bootstrap.php** - Contains global available variables. It's a basic class that's available in the whole proejct and is loaded at the start. Access also through variable $this->baseClass. In the example project, it contains loading of sessions, tokens, and database loading.

  **Config** - the folder contains configuration files in form

  .. code-block:: php
   return array(
       'key' -> 'Value',
       'anotherKey' => 'Another Value'
   );
  In our case, there's also **router.php**, since the example application uses Dframe\Router and **view** folder with the **smarty.php** file, since we used the **S.M.A.R.T.Y** engine, but you can use any system to render html, ex: **Twig, Mustache**, or pure php

  **Controller** - the key file here is **Controller.php** It connects the Router and the earlier mentioned |baseClass|

  Attention!

  - All classes in this folder have to inherit the class that calls to them. 
  |extentionController|
  - Instead of |__construct()| we use the |init()| method - it works in the same way

  **View** - This folder is responsible for the access layer not available directly from the adress.

  - **index.php** can be midified in any way, and methods can be added that will be available in the template - for example, an authorization class. By using |auth()|, you can easily, for example, define the showed content. In the template, the |isLogin()| method is shown by the example of the used engine.
  - **config.php** general configuration that's available for debug, name and version of the application, as well as the adress under which it functions both for dev and the production
 .. div:: col-sm-6
  .. code-block:: bash
   |   composer.json
   |   composer.lock
   |   LICENSE
   |
   +---app
   |   |   Bootstrap.php
   |   |
   |   +---Config
   |   |   |   router.php
   |   |   |
   |   |   \---view
   |   |           smarty.php
   |   |
   |   +---Controller
   |   |       Controller.php
   |   |       Page.php
   |   |
   |   \---View
   |       |   Index.php
   |       |   View.php
   |       |
   |       +---templates
   |           |   footer.html.php
   |           |   header.html.php
   |           |   index.html.php
   |           |
   |           +---errors
   |           |       404.html.php
   |           |
   |           +---page
   |                 test.html.php
   |
   +---vendor
   \---web
       |   config.php
       |   index.php
       |
       +---assets


.. |baseClass| cCode:: $this->baseClass
.. |extentionController| cCode:: extention Controller\Controller
.. |__construct()| cCode:: __construct()
.. |init()| cCode:: init()
.. |auth()| cCode:: $this->assign('auth', new auth());
.. |isLogin()| cCode:: {if $auth->isLogin()} Treść Tylko dla zalogowanej osoby {/if}
