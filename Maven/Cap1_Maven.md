# ¿Qué es Maven?
Maven es un herramienta que proporciona a los desarrolladores un framework completo para la gestión y construccion de software.

Maven provee a los desarrolladores maneras de gestionar:
- Buils
- Documentación
- Reportes
- Dependencias
- SCMs
- Releases
- Distribución
- Mailing List

Los objetivos de Maven son los siguientes:

1. Un modelo de proyecto que sea reutilizable, mantenible y facil de comprender.
2. Plugins y herramientas para poder interactuar con este modelo.

Maven emplea la **Conveción** sobre la **Configuración**, eso quiere decir que los desarrolladores no estan obligados a crear los procesos de compilación ellos mismos. Los desarrolladores no tienen que mencionar todos y cada uno de los detalles de la configuración. Maven proporciona un comportamiento por defecto para los proyectos. Cuando se crea un proyecto *Maven*, este crea una estructura por defecto.

|**Item**|**Por Defecto**|
|--------|---------------|
|*source code*|${basedir}/src/main/java|
|*Resources*|${basedir}/src/main/resources|
|*Test*|${basedir}/src/test|
|*Compilación*|${basedir}/target|
|*Distribución*|${basedir}/target/classes|

### Caracteristicas de *Maven*

- Hasta su configuración más simple sigue las *buenas practicas*.
- Consistencia para usarlo a traves de proyectos.
. Administración de dependencias y actualización.
- Una extensa y creciente lista de repositorios.
- Acceso casi instantáneo a nuevas caracteristicas con una pequeña o inexistente configuración extra.
- **Model-based builds:** *Maven* permite construir cualquier número de proyectos en los tipos predefinidos como .jar, .war, metadata.
- **Información del proyecto:** *Maven* permite generar un sitio web o un dcumento PDF con toda la documentación del proyecto.
- **Gestión de liberaciones y publicación de distribuciones:** Sin ninguna configuración adicional, maven puede integrarse a tu sistema de control de versiones y gestionar las liberaciones de un proyecto.
- **Retrocompatibilidad:** Se puede portar facilmente los modulos de un proyecto a *Maven 3* desde una versión anterior.
- **Versiones padre:** No se necesita especificar el padre en un submodulo para su mantenimiento.
- **Builds Paralelas:** Analiza el gráfico de depencias del proyecto y permite programar builds en paralelo. Usando esto se puede mejorar el rendimiento en un 20%-50%.


