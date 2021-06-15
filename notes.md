# introducción a Laravel

Desarrollo de sistemas web

Entender a laravel como un sistema de capas

![capas](./assets/capas.png)

Para trabajar con PHP necesitamos convertir a nuestro equipo en un servidor web, esto se debe a PHP es un lenguaje del lado del servidor a diferencia de Javascript que es del lado del cliente y funciona bien solo con el navegador.

Del lado del servidor significa que consiste en el procesamiento de una petición de usuario en una computadora llamada servidor web, esta petición se procesa y luego genera páginas en HTML con la respuesta deseada.

## ¿Cómo inicializar un proyecto?

De inicio se hace las instalaciones de VirtualBox y Homestead.

Se configura el archivo homestead.yaml:
- crear llaves ssh
- se configuran la rutas de los shared folders con la carpeta que va a contener los proyectos de laravel:

```
folders:
    - map: C:\Users\Usuario\OneDrive - AURONIX DE MEXICO SAPI  CV\Escritorio\CODE_PROJECTS\laravel-projects\carpeta_de_mi_proyecto
      to: /home/vagrant/laravel-projects/carpeta_de_mi_proyecto
```
}
- en gitbash iniciamos la máquina virtual:
```
$ vagrant up
```

```
$ pwd
/home/vagrant
```

```
$ cd laravel-projects/
```

```
$ composer create-project --prefer-dist laravel/laravel:^7.0 nombre_del_pryecto
```

- modificamos en el archivo homestead.yaml la parte de folders para señalar la ruta del proyecto y también la ruta de sites

```
sites:
    - map: homestead.test
      to: /home/vagrant/laravel-projects/nombre_del_proyecto/public
```

- en archivo hosts añadir la ip de la máquina virtual

- Siempre que se modifique la propiedad sites se debe apagar y prender la maquina virtual

```
vegrant up
vegratn halt
```

## Configurar en homestead múltiples proyectos

Se duplican líneas cambiando la carpeta del proyecto:

```
folders:
    - map: C:\Users\Usuario\OneDrive - AURONIX DE MEXICO SAPI  CV\Escritorio\CODE_PROJECTS\laravel-projects\carpeta_de_mi_proyecto
      to: /home/vagrant/laravel-projects/carpeta_de_mi_proyecto
    - map: C:\Users\Usuario\OneDrive - AURONIX DE MEXICO SAPI  CV\Escritorio\CODE_PROJECTS\laravel-projects\carpeta_de_mi_proyecto_2
      to: /home/vagrant/laravel-projects/carpeta_de_mi_proyecto_2

sites:
    - map: homestead.test
      to: /home/vagrant/laravel-projects/nombre_del_proyecto/public
    - map: homestead.test
      to: /home/vagrant/laravel-projects/nombre_del_proyecto_2/public
```

1. Levantamos la máquina virtual:
```
$ vagrant up
```
2. Ingresamos a la máquina virtual
```
$ vagrant ssh
```
3. Entramos a la carpeta laravel-projects y una vez más creamos un proyecto desde la línea de comandos
```
$ composer create-project --prefer-dist laravel/laravel:^7.0 nombre_del_proyecto_2
```
4. si necesitamos una base de datos más entonces:
```
databases:
    - homestead
    - nombre_del_proyecto_2
```
5. Reinciamos la máquina virtual
```
$ vagrant reload --provision
```

6. En el arhivo hosts añadir el nuevo dominio, misma ip solo cambio de nombre
```
192.168.10.10   homestead.test
192.168.10.10   nombre_del_proyecto_2.test
```

7. Se prueba en el nuevo dominio

8. Abrimos el folder contenedor del nuevo proyecto y en el archivo .env configuramos la base de datos:
```
DB_DATABSE=nombre_del_proyecto_2
DB_USERNAME=homestead
DB_PASSWORD=secret
```
