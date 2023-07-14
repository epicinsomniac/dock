```  nginx:
   container_name: nginx-app
   image: nginx:latest
   env_file:
     - ${DROOT}/.env
   expose:
     - 80
   volumes:
     - $DAPPS/nginx/var/www/html:/var/www/html
     - ${DAPPS}/nginx/default.conf:/etc/nginx/conf.d/default.conf
   links:
     - php-fpm
   #networks:
     #- routing

  php-fpm:
    container_name: php-fpm
    image: nanoninja/php-fpm
    volumes:
      - $DAPPS/nginx/var/www/html:/var/www/html
    networks:
      - routing
```
