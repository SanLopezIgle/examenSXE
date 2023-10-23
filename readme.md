# Examen SXE (prestashop)
En este examen vamos a poner en marcha PrestaShop.

- Usaremos la imagen prestashop
```
docker pull prestashop/prestashop
```

- Creamos nuestro **docker-compose.yml** que nos quedara configurado de la siguiente manera:
```
services:

  prestashop:
    image: prestashop/prestashop
    ports:
      - "8081:80"
    environment:
      PRESTASHOP_HOST: mariadb
      PRESTASHOP_DB_USER: prestashop
      PRESTASHOP_DB_PASSWORD: prestashop
      PRESTASHOP_DB_NAME: prestashop
    volumes:
      - prestashop_data:/var/www/html
    depends_on:
      - mariadb
    links:
      - mariadb

  mariadb:
    image: mariadb
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: prestashop
      MYSQL_USER: prestashop
      MYSQL_PASSWORD: prestashop
    volumes:
      - mariadb_data:/var/lib/mysql
    #expose:
     # - 3306
      #- 33060
    ports:
      - "3306:3306"

volumes:
  prestashop_data:
  mariadb_data:
```

- Iniciamos los contenedores de PrestaShop y MariaDB en segundo plano:
```
docker-compose up -d
```

- Accedemos a Prestashop desde nuestro navegador: 
```
http://localhost:8081
```

![prestashop](/home/dam2/Imágenes/prestashop.png)

**- Base de datos enlazados al PhpStorm**

No me funciona la conexión con la base de datos, el error que me da es el que aparece en la imagen que adjunto a continuación:

![phpstorm](/home/dam27Imágenes/php.png)

Tenemos que asegurarnos de que la manera en la que nombremos a todo en el archivo **.yml** coincide con como lo nombreros a la hora de crear la conexión con la base de datos