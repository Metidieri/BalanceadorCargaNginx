# BalanceadorCargaNginx
## Configuración de las máquinas virtuales
### Le asignamos las IPs y scripts a las máquinas
![](CapturasNginx/Captura0.PNG)
### A continución muestro los scripts
![]()
![]()
![]()
## MÁQUINA MYSQL
### cd /etc/mysql/mariadb.conf.d/
### sudo nano 50.server.cnf
![](CapturasNginx/Captura1.PNG)
### Dentro de archivo cambiamos lo siguiente, poniendo la IP de la maquina MYSQL
![](CapturasNginx/Captura2.PNG)
### Ahora ponemos una contraseña al root de el MYSQL
### sudo nano mysql_secure_installation
![](CapturasNginx/Captura3.PNG)
### Entramos a la base de datos
### Creamos el usuario, le damos privilegios y acabamos con un flush privileges
![](CapturasNginx/Captura4.PNG)
### Descargamos del gihub con el enlace el archivo
![](CapturasNginx/Captura5.PNG)
### Importamos la base de datos al MYSQL
![](CapturasNginx/Captura6.PNG)
## MÁQUINAS NGINX
# IMPORTANTE
## Los pasos mostrados deben de seguirse en ambas máquinas
### cd /var/www/
### sudo mkdir sitiopedro
### sudo chown www-data.www-data sitiopedro/
![](CapturasNginx/Captura7.PNG)
### Descargamos el archivo del github
![](CapturasNginx/Captura8.PNG)
### Entramos en la carpeta descargada
### cd src/
### sudo mv * /var/www/sitiopedro/
![](CapturasNginx/Captura9.PNG)
### Editamos el archivo config.php y ponemos la IP de la base de datos
![](CapturasNginx/Captura10.PNG)
### cd /etc/php/7.4/fpm/pool.d
### sudo nano www.conf
![](CapturasNginx/Captura12.PNG)
### Cambiamos la dirección que nos aparece en listen por la siguinete dirección
![](CapturasNginx/Captura11.PNG)
### Reiniciamos el php y hacemos una copia del default en el sites-available, además lo editamos
![](CapturasNginx/Captura13.PNG)
### Dentro del archivo cambiamos html por sitiopedro y despues de el primer index añadimos index.php
![](CapturasNginx/Captura14.PNG)
### Más abajo en el mismo archivo tenemos que descomentar las lineas como en la captura
![](CapturasNginx/Captura15.PNG)
### Creamos un enlace con el siguiente comando
### sudo ln -s /etc/nginx/sites-available/sitionginx /etc/nginx/sites-enabled/sitionginx
### Tambien borramos el default
![](CapturasNginx/Captura16.PNG)
### sudo nginx -t
### sudo systemctl restart nginx
![](CapturasNginx/Captura17.PNG)
## MÁQUINA BALANCEADOR
### cd /etc/nginx/sites-enabled/
### sudo rm default
### sudo nano conf.d
![](CapturasNginx/Captura18.PNG)
### Dentro del archivo que hemos creado añadimos lo siguiente, poniendo las IPs de los nginx
![](CapturasNginx/Captura19.PNG)
### Movemos el archivo hasta el sitio que le corresponde
### sudo mv /etc/nginx/sites-available/conf.d /etc/nginx/conf.d/confbalanceador.conf
![](CapturasNginx/Captura20.PNG)