.. div:: row
 .. div:: col-md-6
  |img/restful.jpg|

 .. div:: col-sm-6
  Friendly links
  ^^^^^^^^^^^^^^^

  For safety reasons, it's recommended in the production version to use.
  |listing|

.. |img/restful.jpg| router:: img/restful.jpg
 :publicWeb:
 :img:
 :width: 100%


.. |listing| customLi:: myTab
 :apache2: Apache (.htaccess)
 :nginx: active/Nginx (.conf)
  .. code-block:: apache
   RewriteEngine On
   
   #Deny access for hidden folders and files
   RewriteRule (^|/)\.([^/]+)(/|$) - [L,F]
   RewriteRule (^|/)([^/]+)~(/|$) - [L,F]
   
   #Set root folder to web directory
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^(.*)$ web/$1
   
   #Redirect all queries to index file
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^(.*)$ web/index.php [QSA,L]
  next
  .. code-block:: nginx
  
   #Set root folder to web directory
   location / {
       root   /home/[project_path]/htdocs/web;
       index  index.html index.php index.htm;
       if (!-e $request_filename) {
           rewrite ^/(.*)$ /index.php?q=$1 last;
       }
   }
   
   #Redirect all queries to index file
   location ~ .php$ {
       try_files $uri = 404;
       fastcgi_pass 127.0.0.1:9000;
       #fastcgi_pass unix:/run/php/php7.1-fpm.sock;
       fastcgi_index web/index.php;
       fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
       include fastcgi_params;
   }
