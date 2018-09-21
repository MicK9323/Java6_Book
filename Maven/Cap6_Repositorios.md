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

Cuando Maven no encuentra una dependencia en el repositorio local, este comienza a buscar en el repositorio central a través de la siguiente *URL: http://repo1.maven.org/maven2/*

- Este repositorio es administrado por la comunidad de Maven.
- No requiere configuración.
- Requiere de una conexión a internet para que pueda realizar la busqueda de dependencias.

## Repositorio Remoto

En ocasiones Maven no encontrará una dependencia en el repositorio central, por consiguiente detendra el proceso de compilación y mostrara un mensaje de error en la consola. Para prevenir situaciones como esta, Maven nos da el concepto de *Repositorios Remotos*, los cuales son de propiedad del desarrollador y puede contener las dependencias necesarias o *jars* de otros proyectos.

Por ejemplo usando la siguiente configuración en el POM, Maven podrá descargar librerias desde el repositorio indicado en la configuración.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.companyname.projectgroup</groupId>
    <artifactId>project</artifactId>
    <version>1.0</version>

    <dependencies>
        <dependency>
            <groupId>com.companyname.common-lib</groupId>
            <artifactId>common-lib</artifactId>
            <version>1.0.0</version>
        </dependency>
    <dependencies>

    <repositories>
        <repository>
            <id>companyname.lib1</id>
            <url>http://download.companyname.org/maven2/lib1</url>
        </repository>
        <repository>
            <id>companyname.lib2</id>
            <url>http://download.companyname.org/maven2/lib2</url>
        </repository>
    </repositories>

</project>
```

## Secuencia de Busqueda de Maven

Cuando ejecutamos el comando *build*, Maven empieza a buscar las librerias en la siguiente secuencia:

1. Busca las dependencias en el repositorio local, si no las encuentra, pasa al paso 2.
2. Busca y descarga las dependencias desde el repositorio central, si no las encuentra y hay repositorios remotos definidos en el POM, pasa al paso 4.
3. Si han fallado las busquedas anteriores y no hay repositorios remotos definidos en el POM, se detiene el proceso de compilación y se lanza el error: *Unable to find dependency*.
4. Busca y descarga las dependencias desde el repositorio remoto. Caso contrario detiene el proceso y lanza el error *Unable to find dependency*.
