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

Un *goal* representa una tarea específica que contribuye a la construcción y gestión de un proyecto. Un *goal* puede estar ligado a ninguna o muchas fases.

El orden de ejecución depende del orden en que los *goals* y las fases son invocadas.

```cmd
mvn clean dependency:copy-dependency package
```

