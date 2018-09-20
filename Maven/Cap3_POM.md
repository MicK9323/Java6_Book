# Capitulo 3: POM

POM acrónimo para ***Project Object Model***. Es la unidad fundamental para trabajar en *Maven*. Es un archivo *xml* que se ubica en el directorio base del proyecto como *pom.xml*.

El POM contiene la información acerca del proyecto y el detalle de la configuración que usara *Maven* para construir el proyecto.

Algunas de las configuraciones que se pueden especificar en POM son las siguientes:

- Dependencias del proyecto.
- Plugins.
- Goals.
- Build profiles (Perfiles de construcción).
- Versión del proyecto.
- Desarrolladores.
- Mailing List.
  
Antes de crear un POM debemos especificar el grupo del proyecto (**groupId**), su nombre (**artifactId**) y la versión. Estos atributos atributos ayudaran a identificar el proyecto dentro de un repositorio.

Ejemplo de un POM

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.companyname.project-group</groupId>
    <artifactId>project</artifactId>
    <version>1.0</version>

</project>
```
Cabe señalar que solo existira un archivo POM para cada proyecto.

- Todos los archivos POM requieren de 3 elementos obligatorios: **groupId**, **artifactId** y **version**
- La notación de un proyecto dentro de un repositorio es: **groupId:artifactId:version**.
- Los requisitos mínimos para un archivo POM son:
  
  |**Nodo**|**Descripción**|
  |--------|---------------|
  |*Project root*|Esta es la etiqueta raiz. Se tiene que especificar la configuración del esquema como el esquema de apache y la definición de w3.org|
  |*Model version*|El *model version* Debera ser 4.0.0|
  |*groupId*|Este un ID del grupo del proyecto. Es generalmente único entre una organización o un proyecto.|
  |*artifactId*|Este un ID para el proyecto. Es generalmente el nombre del proyecto|
  |*version*|Esta es la versión del proyecto. Es usado dentro de un repositorio de *artifacts* para separarlas de las demas versiones.|

## Super POM
El super POM es el POM por defecto de *Maven*. Todos los POMs heredan de un padre o un POM base. Esta base es conocida como **Super POM** y contiene valores heredados por defecto.

Una forma facil de ver las configuraciones por defecto es ejecutando el comando: ***mvn help:effective-pom.***

Esto generará un fichero xml con la estructura por defecto del proyecto, directorios de salida, plugins necesarios, repositorios, directorio de reportes que *Maven* usará mientras ejecuta un *goal* (meta).
