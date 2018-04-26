# Instalar Django en vagrant desde cero

Guia de instalacion desde cero
Crear carpeta donde se alojara el proyecto.
>mkdir 'project_name'

## Configurar puertos

Desde el archivo de *vagrantfile* escribir lo siguiente:

```ruby
config.vm.network "forwarded_port", guest:80, host: 8080
config.vm.network "forwarded_port", guest:8000, host: 8081
```

## Sincronizar carpeta de proyecto desde el vagrantfile

```ruby
config.vm.synced_folder "C:/ruta/proyecto/local", "/home/vagrant/nombre_carpeta_proyecto"
```

### Teniendo configurado la carpeta arrancamos vagrant

>vagrant up
>
>vagrant ssh

### Dirigirse a la carpeta del proyecto en vagrant

>cd project_name/

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

**activar si no lo esta*

>source 'name'/bin/activate

## Instalar Django con pip

>pip install django

## Instalar Requeriments.txt

>pip install -r Requeriments.txt

## Crear proyecto Django

>django-admin startproject mysite
>
>Cambie el directorio externo mysite y ejecute lo siguiente
>
> python manage.py runserver 'ip:port'
>

Bien! Hasta este paso podemos arrancar el servidor correctamente. Sigue crear una app en nuestro proyecto.

## Crear app en django

Estando posicionados en la carpeta del proyecto escribimos lo siguiente
>python manage.py startapp 'nombre_app'
