# Instalar Django en vagrant desde cero

Guia de instalacion desde cero.
Crear carpeta donde se alojara el proyecto.

>mkdir 'project_name'

## Configurar puertos

Desde el archivo de *vagrantfile* escribir lo siguiente:

```ruby

config.vm.network  "forwarded_port", guest:80, host: 8080

config.vm.network  "forwarded_port", guest:8000, host: 8081

```

## Sincronizar carpeta de proyecto desde el vagrantfile

```ruby

config.vm.synced_folder  "C:/ruta/proyecto/local", "/home/vagrant/nombre_carpeta_proyecto"

```

**Teniendo sincronizada la carpeta, arrancamos vagrant.**

**Dirigirse a la carpeta del proyecto en vagrant**  ```$ cd project_name/```

## Instalar pip en caso de no tenerlo

> sudo easy_install pip

## Instalar python

> sudo apt-get -y install python-pip python-dev build-essential python-virtualenv

## Instalar *(si es necesario)* MysqlClient MysqlServer

> sudo apt-get -y install mysql-client mysql-server sqlite3
> sudo apt-get -y install python-mysqldb libmysqlclient-dev python-mysql.connector

## Crear entorno virtual (Virtualenvs)

>cd project_name/
>virtualenv 'name'
>
**activar, si no lo esta.**
>source 'name'/bin/activate

```
(name)vagrant@fernando:-$
```

*Para desactivar el entorno virtual usar el comando ```deactivate ```*

## Agregar variables de entorno
Al tener las variables de entorno nos dirigimos al archivo ```postactivate``` . Este archivo se encuentre en ```~/.virutalenvs/project_name/bin/postactivate```
```
#!/bin/bash

export DB_NAME='yourdata'
export DB_USER='yourdata'
export DB_PASSWORD='yourprivatepassword'
export SECRET_KEY='youruniqueunpredictablevalue'
export DB_HOST='yourhost'

#-- secret key EMAIL
export EMAIL_HOST='yourhost'
export EMAIL_USER='yourdata'
export EMAIL_PASSWORD='yourprivatepassword'
export EMAIL_PORT='port'
export EMAIL_DEFAULT='youremail'

```

## Instalar Django con pip

>pip install django

## Instalar requeriments

>pip install -r Requeriments.txt

## Crear proyecto Django
```
$ django-admin startproject mysite
```

>Cambie el directorio externo mysite y ejecute lo siguiente
``` 
$ python manage.py runserver 'ip:port'
```

**Bien! Hasta este paso podemos arrancar el servidor correctamente. Sigue crear una app en nuestro proyecto.**

## Crear app en django
Al crear una app  debemos estar posicionados en la carpeta del proyecto. Ejecutamos el siguiente comando:

```
$ python manage.py startapp 'nombre_app'
```

Al crearse una app, debemos especificarle a django que la integre a nuestro proyecto, desde el ```settings.py ```:
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'appname',
]
```
Ahora django sabe incluir nuestra aplicación.
Ejecutamos migraciones con el siguiente comando:
```
$ python manage.py makemigrations
```
Después que creamos una migración la ejecutamos con el siguiente comando para aplicar cambios a la base de datos:
```
$ python manage.py migrate
```

## Crear un usuario del admin
Primero tendremos que crear un usuario para poder iniciar sesión en el admin. Ejecutamos el siguiente comando:
```
$ python manage.py createsuperuser 
```
A continuación nos pedirá nuestro nombre de usuario con el cual nos logearemos: 
```
Username: admin
```
A continuación nos pedirá nuestra dirección de correo:
```
Email address: admin@example.com
```
El paso final es crear nuestra contraseña para ingresar:
```
Password: ***
Password (again): ***
Superuser created successfully
```

### Iniciamos el servidor
```
$ python manage.py runserver '0:8000'
```

En el navegador colocamos la ruta:
>ip_address:8000/admin

Así ingresamos al panel de admin y hacemos Log in con nuestro usuario admin.

Ya hasta este paso podemos ingresar con nuestro usuario __admin__ al sitio de administrador que nos facilita Django. El paso siguiente es crear modelos, vistas, configurar urls, etc...