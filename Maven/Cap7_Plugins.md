# Capitulo 7: Plugins

## ¿Qué son los plugins de maven?

Maven es, de manera práctica, un framework de ejecución de plugins, donde cada tarea es realizada por un plugin.

Estos plugins generalente se usan para:

- Crear paquetes *jar*.
- Crear paquetes *war*.
- Compilar archivos de código.
- Pruebas unitarias de código.
- Crear la documentción de un proyecto.
- Crear reportes de proyectos.

Un *plugin* generalmente proporciona un juego de *goals*, que pueden ser ejecutados usando la siguiente sintáxis.

```cmd
mvn [plugin-name]:[goal-name]
```

Por ejemplo un proyecto java puede ser compilado ejecutando el siguiente comando:

```cmd
mvn compiler:compile
```

Maven tiene 2 tipos de plugins:

1. ***Build plugins:*** Son ejecutados durante el proceso de compilación y pueden ser configurados dentro del elemento *\<build/\>* del *pom.xml*.
2. ***Plugins de Reportes:*** Son ejecutados en el proceso *site* y pueden ser configurados dentro del elemento *\<reporting/\>* del *pom.xml*.

Los plugins más usados en maven son:

|    **Plugin**    |    **Descripción**    |
|------------------|-----------------------|
|*clean*|Limpia el directoro *target* luego de la compilación. Elimina el directorio *target*.|
|*compiler*|Compila código fuente de Java|
|*surefire*|Ejecuta las pruebas unitarias *JUnit*. Crea un reporte del *test*|
|*jar*|Compila un paquete *jar* del proyecto actual.|
|*war*|Compila un paquete *war* del proyecto actual.|
|*javadoc*|Genera la documentación del proyecto|
|*antrun*|Ejecuta un conjunto de tareas de *ant* de cualquier fase de compilación.|

Ejemplo:
Crearemos el siguente archivo pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.companyname.projectgroup</groupId>
    <artifactId>project</artifactId>
    <version>1.0</version>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                    <id>id.clean</id>
                    <phase>clean</phase>
                    <goals>
                        <goal>run</goal>
                    </goals>
                    <configuration>
                        <tasks>
                            <echo>clean phase</echo>
                        </tasks>
                    </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>
```

Luego abriremos la consola de comandos y nos ubicaremos en la carpeta que contiene el archivo *pom.xml* y ejecutaremos el comando.

```cmd
mvn clean
```

Maven iniciará el proceso y mostrará la fase *clean* del ciclo de vida *clean*.

```cmd
[INFO] Scanning for projects...
[INFO] -----------------------------------------------------------------
-
[INFO] Building Unnamed - com.companyname.projectgroup:project:jar:1.0
[INFO] task-segment: [post-clean]
[INFO] -----------------------------------------------------------------
-
[INFO] [clean:clean {execution: default-clean}]
[INFO] [antrun:run {execution: id.clean}]
[INFO] Executing tasks
[echo] clean phase
[INFO] Executed tasks
[INFO] -----------------------------------------------------------------
-
[INFO] BUILD SUCCESSFUL
[INFO] -----------------------------------------------------------------
-
[INFO] Total time: < 1 second
[INFO] Finished at: Sat Jul 07 13:38:59 IST 2012
[INFO] Final Memory: 4M/44M
[INFO] -----------------------------------------------------------------
-
```

Los ejemplos anteriores describen los siguientes conceptos:

- Los *plugins* son especificados dentro del pom.xml, usando los elementos *\<plugins/\>* y *\<plugin/\>*.
- Cada *plugin* puede tener multiples *goals*.
