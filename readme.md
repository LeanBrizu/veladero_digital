# Veladero Digital

Este proyecto contiene una configuración de Docker Compose para poner en marcha una aplicación web llamada "Veladero Digital". La aplicación utiliza PHP 5.6.40 con el servidor web Nginx y una base de datos MariaDB.

# Estructura de archivos

La estructura de archivos del proyecto es la siguiente:

scss

/srv/http/veladero_digital
├── app/
│   ├── config/
│   │   ├── (archivos de configuración de tu aplicación)
│   ├── public/
│   │   ├── (archivos accesibles públicamente de tu aplicación)
│   ├── src/
│   │   ├── (código fuente de tu aplicación)
│   ├── shared_sessions/
│   │   ├── (archivos de sesión compartidos de CodeIgniter)
│   ├── Dockerfile
│   ├── (otros archivos específicos de tu aplicación)
├── database/
│   ├── (archivos o scripts de la base de datos)
├── nginx/
│   ├── nginx.conf
│   ├── logs/
├── php/
│   ├── php.ini
├── docker-compose.yml
├── readme.md

# Configuración de Docker Compose

El archivo docker-compose.yml contiene la configuración de los servicios necesarios para ejecutar la aplicación:
Servicio "app":

    Se construye a partir del archivo Dockerfile ubicado en la carpeta app/.
    Se expone en el puerto 80.
    Utiliza volúmenes para montar los directorios locales necesarios para el funcionamiento del servidor web Nginx, la base de datos y la configuración de PHP.
    Ejecuta el comando "nginx", "-g", "daemon off;" para iniciar el servidor Nginx.
    Depende del servicio "db" para asegurar que la base de datos esté disponible antes de que se inicie la aplicación.

Servicio "db":

    Utiliza la imagen de MariaDB para el servicio de base de datos.
    Configura la contraseña de root para la base de datos como "root".
    Se expone en el puerto 3306.
    Utiliza un volumen para montar el directorio local database para almacenar los archivos de la base de datos.

# Archivo Dockerfile

El archivo Dockerfile ubicado en la carpeta app/ contiene las instrucciones para construir la imagen del servicio "app". Las acciones que se realizan en el Dockerfile incluyen:

    Instalar Nginx y OpenRC para el servidor web.
    Instalar el cliente de MariaDB para interactuar con la base de datos.
    Instalar la extensión de PHP "mysqli" para la comunicación con la base de datos.
    Configurar el archivo php.ini para PHP.
    Copiar la configuración de Nginx desde nginx/nginx.conf.
    Copiar los archivos de la aplicación desde app/src a la ruta /var/www/html dentro del contenedor.
    Crear el directorio /run/nginx necesario para Nginx y establecer permisos adecuados.
    Iniciar PHP-FPM como el proceso principal del contenedor.

# Puesta en marcha del proyecto

Para poner en marcha la aplicación, asegúrate de tener Docker y Docker Compose instalados en tu sistema. Luego, ejecuta el siguiente comando en el directorio raíz del proyecto:

docker-compose up -d

Esto construirá las imágenes y ejecutará los servicios necesarios. Podrás acceder a la aplicación a través del puerto 80 en tu navegador web.