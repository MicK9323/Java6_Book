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

