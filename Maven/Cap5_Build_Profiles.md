# Capitulo 5: Perfiles de Compilación

## ¿Qué es un perfil de compilación?
Un perfil de compilacion (*build profile*) es un conjunto de configuraciones, que pueden ser usadas para *settear* o sobreescribir valores por defecto en una compilación de Maven. Usando perfiles de compilación podemos customizar la compilación para diferentes ambientes como *Ambiente de Produccion* y *Ambiente de desarrollo*.

Los perfiles son especificados en el archivo *pom.xml* usando los elementos *activeProfile* y *profiles*.

## Tipos de perfiles de compilación

Son mayormente de 3 tipos:

|    Tipo    |        Donde son definidos        |
|------------|-----------------------------------|
|Por Proyecto|Definido en el POM del proyecto (*pom.xml*)|
|Por Usuario|Definido en la configuración de Maven (%USER_HOME%/.m2/settings.xml)|
|Global|Definido en la configuración global de Maven (%M2_HOME%/conf/settings.xml)|

## Activación de los perfiles.

Los perfiles de compilación pueden ser activados de distintas formas:

- Explícitamente usando comandos de consola.
- A través de la configuración de Maven.
- Basado en variables de entorno (Variables de Usuario).
- Configuraciones del sistema operativo.

*Buscar otras fuentes sobre builds profiles*