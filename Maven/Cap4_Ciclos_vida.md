# Capítulo 4: Ciclo de Vida de Compilación

## ¿Qué es el ciclo de vida de compilación?
Puede ser definido como una secuencia de fases que definen el orden en que los *goals* seran ejecutados. Estas fases representan un nivel en el ciclo de vida.

Como ejemplo podemos ver que el ciclo de vida de una compilación típica de Maven consiste en las siguientes secuencias de fases.

|    **Fase**    |    **Función**    |    **Descripción**    |
|----------------|-------------------|-----------------------|
|*prepare-resource*|**Preparar Recursos**|La copia de los recursos puede ser customizada en esta fase|
|*validate*|**Validación**|Validar si el proyecto esta correcto y si esta disponible toda la información|
|*compile*|**Compilación**|El código fuente es compilado en esta fase|
|*test*|**Pruebas**|Prueba del código fuente compilado|
|*package*|**Empaquetado**|Se crean los JAR/WAR según este indicado en el POM.xml|
|*install*|**Instalación**|Se instala el paquete en un repositorio local o remoto de maven|
*deploy*|**Despliege**|Copia el paquete final al repositorio remoto|

Maven tiene 3 fases estandar:

- *clean*
- *default o build*
- *site*

Un *goal* o meta representa una tarea específica que contribuye a la construcción y gestión de un proyecto. Un *goal* puede estar ligado a ninguna o muchas fases.

El orden de ejecución depende del orden en que los *goals* y las fases son invocadas.

```cmd
mvn clean dependency:copy-dependency package
```

Teniendo en cuenta el comando anterior. Los argumentos *clean* y *package* son fases de compilación mientras que *dependency:copy-dependency* es un *goal*. Donde *clean* es la primera fase en ser ejecutada, seguida de *dependency:copy-dependency* y por último se ejecuta la fase *package*.

## Ciclo de Vida *clean*
Cuando ejecutamos el comando *mvn post-clean*, Maven invoca el ciclo de vida *clean*, la cual contiene las siguientes fases.

- *pre-clean*
- *clean*
- *post-clean*

El *goal* de maven *clean:clean* esta ligado a la fase *clean* del ciclo de vida *clean*. La sintaxis de la invocación es *clean*:*pre-clean|clean|post-clean*. Así que cuando ejecutamos el comando *mvn clean*, maven borra el directorio de compilación.

## Ciclo de Vida *Build* o *Default*

Este es el ciclo primario de Maven y es usado para compilar las aplicaciones. Tiene 23 fases.

|**Fase**|**Descripción**|
|--------|---------------|
|*validate*|Valida si el proyecto está correcto y si dispone de toda la información para completar el proceso de compilación.|
|*initilize*|Inicializa el estado de compilación|
|*generate-sources*|Genera el código fuente para ser incluido en la fase de compilación|
|*process-sources*|Procesa el código fuente|
|*generate-resources*|Genera los recursos que seran incluidos en el empaquetado|
|*process-resources*|Copia y procesa los recursos dentro del directorio destino.|
|*compile*|Compila el código fuente del proyecto|
|*process-classes*|Posprocesado de los archivos generados en la compilación|
|*generate-test-sources*|Genera el código fuente de prueba para ser incluido en la fase de compilación.|
|*process-test-sources*|Procesa el codigo fuente de prueba|
|*test-compile*|Compila el código fuente de prueba en el directorio destino|
|*process-test-classes*|Procesa los archivos generados en el *test-compile*|
|*test*|Ejecuta las pruebas usando el framework de pruebas adecuado|
|*prepare-package*|Realiza toda operación necesaria para preparar un paquete antes de que este sea empaquetado|
|*package*|Toma el código compilado y lo empaqueta en un formato distribuible como *JAR*, *WAR* o *EAR*.|
|*pre-integration-test*|Realiza las acciones necesarias antes de que las pruebas de integración sean ejecutadas|
|*integration-test*|Procesa y despliega el paquete dentro de un ambiente donde las pruebas de integración puedan ser ejecutadas.|
|*post-integration-test*|Realiza las acciones requeridas luego que las pruebas de integración han sido ejecutadas|
|*verify*|Verifica que el paquete sea válido y que cumple con los criterios de calidad.|
|*install*|Instala el paquete dentro del repositorio local,el cual podrá ser usado como una dependencia en otros proyectos locales.|
|*deploy*|Copia el paquete final a un repositorio remoto para que pueda ser compartido con otros desarrolladores y usado en otros proyectos.|

Hay algunos conceptos relacionados a *Maven* los cuales dicen que:

- Cuando una fase es llamada por un comando Maven por ejemplo *mvn compile*, solo se ejecutarán esta fase y las que sigan luego de esta.
- Diferentes *Maven goals* podran ser ligados a diferentes fases del ciclo de vida de Maven dependiendo del tipo de empaquetado (JAR/WAR/EAR).

## Ciclo de Vida *Site*

El plugin *site* de maven es generalmente usado para generar documentación, reportes, sitios de despliege, etc.

Tiene las siguientes fases:

- *pre-site*
- *site*
- *post-site*
- *site-deploy*

*Buscar más fuentes sobre el plugin site*
