# Capitulo 6: Repositorios

## ¿Qué es un repositorio de Maven?

En la terminología de Maven, un repositorio es un directorio donde todos los proyectos, librerias, plugins o cualquier otro artefacto son almacenados y pueden ser usados por MAven de una forma sencilla.

Los repositorios de Maven son de 3 tipos:

- local
- central
- remota

## Repositorio Local

El repositorio local de Maven es una carpeta ubicada en nuestra maquina y es creada la primera vez que ejecutamos algun comando de Maven.

Este almacena todas las dependencias de los proyectos (librerias, plugins, etc). Cuando se ejecuta una compilación, Maven descarga las dependencias dentro del repositorio local. Esto ayuda a evitar referencias a repositorios remotos cada vez que un proyecto es compilado.

Maven crea por defecto el repositorio local dentro de la carpeta *%USER_HOME%*. Para sobreescribir la ubicación por defecto se debe cambiar el atributo dentro del archivo *settings.xml* ubicado en la carpeta *%M2_HOME%\conf*

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
          http://maven.apache.org/xsd/settings-1.0.0.xsd">

    <localRepository>C:/MyLocalRepository</localRepository>

</settings>
```

Cuando se vuelva a ejecutar un comando Maven, se descargaran las dependencias dentro de la carpeta en la ruta especificada.

## Repositorio Central

El repositorio central de maven, es un repositorio suministrado por la comunidad de Maven. Y contiene un largo número de librerias comunmente usadas.


