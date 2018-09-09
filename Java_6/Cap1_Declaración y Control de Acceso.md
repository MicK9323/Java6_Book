# CAPITULO 1: Declaración y Control de Acceso

### Temas a tratar:
- Declaración de clases e interfaces.
- Desarrollar clases e interfaces.
- Uso de datos primitivos, arreglos, enums e identificadores.
- Métodos estáticos, nomenclatura javabean, argumentos y variables.

## 1. Introducción
___
Un programa Java es básicamente una colección de objetos que se comunican entre sí invocando los métodos de cada uno. Cada objeto es de un cierto tipo, este tipo esta definido por una clase o una interfaz.

- **Clase:** Es una plantilla que describe los estados, atributos y comportamientos que soportará un tipo de objeto.
- **Objeto:** Es la instancia de una clase creada por la JVM, cuando encuentra la palabra clave *new* crea un objeto que es una instancia de la Clase. Este objeto puede tener su propio estado, atributos y comportamiento definidas en su clase.

### Identificadores y Keywords (Palabras Clave)
Todos los componentes en Java necesitan un nombre, estos nombres son llamados ***Identificadores*** y hay una serie de reglas que constituyen un identificador válido Java.
### Herencia
Tanto en Java como en otros lenguajes orientados a objetos, existe el concepto de herencia. Esto permite que el código definido en una clase pueda ser reutilizada en otra clase. En Java, podemos definir una superclase general y luego ampliarla con subclases más especificas. Una subclase que hereda de una superclase tiene acceso automático a las variables y métodos definidos en la superclase, pero es libre de sobreescribir los métodos para definir comportamientos más específicos.
### Interfaces
Las interfaces son como una superclase abstracta que define que métodos deberá soportar una subclase, pero no como debe ser soportada.
## 2. Identificadores y JavaBeans
___
Los identificadores de Java deben cubrir los siguiente:
- **Identificador válido:** Las reglas que el compilador usa para determinar si un nombre es válido.
- **Convenciones:** Recomendaciones de Sun para nombrar clases, variables y métodos.
- **Nomenclatura Estandar JavaBean:** Reglas básicas para la nomenclatura de los JavaBeans.

### **Identificador Válido**
Tecnicamente los identificadores solo deben estar compuestas por carácteres, números, simbolos de moneda y conectores (_). Las reglas a cumplir son las siguentes:
+ Debe comenzar con una letra, un símbolo de moneda ($) o un conector como el guión bajo (_). No pueden comenzar con un número.
+ Despues del primer carácter los identificadores pueden contener cualquier combinación de letras, simbolos de moneda, conectores y números.
+ No hay límite para la cantidad de caracteres que un identificador puede contener.
+ No se puede usar una palabra reservada de Java como identificador.
+ Los identicadores en Java son case-sensitive

```java
// Identificadores válidos
int _a;
int $c;
int ______2_w;
int _$;
int this_is_a_very_detailed_name_for_an_identifier;

// Identificadores inválidos
int :b;
int -d;
int e#;
int .f;
int 7g;
```

### **Convenciones de Sun Microsystems**
1. **Clases e Interfaces:** La primera letra debe ser mayúscula, si es un nombre compuesto por varias palabras, estas deben estar unidas estando la primera letra de cada una en mayúscula.

```java
Dog
Account
PrintWriter
```
Para nombrar interfaces, los nombres pueden ser adjetivos como:
```java
Runnable
Serializable
```
2. **Métodos:** La primera letra debe ser minúscula y seguir el formato camelCase.
```java
getBalance
doCalculation
doSomething
setProviderName
```
3. **Variables:** Al igual que en los métodos debe empezar con minúscula y seguir el formato camelCase.
```java
buttonWidth
accountBalance
firstName
```
4. **Constantes:** Las constantes en Java son creadas marcando una variable como ___static___ y ___final___. Deben estar en mayúsculas y separarse con (_) si tuviera un nombre compuesto.
```java
static final int MAX_HEIGHT
static final String URL_ENDPOINT
```
### **Estandar JavaBean**
Los JavaBean son clases de Java que tienen propiedades o atributos. Para este propósito pensaremos en estos atributos o propiedades como variables privadas. Al ser privadas, el unico modo de acceder a ellas desde afuera de su clase, es a través de métodos. Los métodos que permiten cambiar el valor de una propiedad son llamados ___setter___ y los métodos que devuelven el valor de una propiedad son llamados ___getter___.
#### Reglas para nombrar las propiedades de un JavaBean
- Si la propiedad no es de tipo ___boolean___, el método ___getter___ debe tener el prefijo ___get___. Por ejemplo ___getSize()___ , ___getLastName()___
- Si la propiedad es de tipo ___boolean___, el prefijo del método ___getter__ debe ser ___get___ o ___is___ (recomedable que sea __is__ aunque ambos son válidos). Por ejemplo ___isHigherThan()__ , ___isCompleted()___
- El prefijo de los métodos ___setter___ debe ser ___set___. Por ejemplo ___setSize()___
- Para completar el nombre de un método ___getter___ o ___setter___, cambiar la primera letra del nombre de la propiedad a mayúscula y concatenarla al prefijo ___get___, ___set___ o ___is___
- Los métodos ___setter___ deben ser marcados como ___public___ y de tipo ___void___.
- Los métodos ___getter___ deben ser marcados como ___public___ y deberan retornar el tipo de dato de la propiedad que encapsula.

***Los objetivos para el examen dicen que se tienen que conocer los identificadores válidos solo para las variables, pero las reglas son las mismas para todos los componentes Java. Entonces debemos recordar que un identificador válido para una variable es tambien válido para un método o una clase. Sin embargo necesitamos distinguir entre identificadores válidos y convenciones de nomenclatura, como el estandar JavaBean, que indica como debe ser nombrado un componente JavaBean. En otras palabras deberemos poder reconocer que un identificador es válido así no cumpla con los estándares de nomenclatura.***

## 3. Declaración de Clases
___
Cuando escribimos código Java, escribiremos Clases o Interfaces. Dentro de estas clases, como ya sabemos, habrá variables y métodos. Como declaremos las clases, variables y métodos afectará dramaticamente el comportamiento del código de la aplicación. Por ejemplo un método ***public*** puede ser accedido desde cualquier parte del código de nuestra aplicación. Para este fin estudiaremos las formas en que podremos declarar y modificar (o no) una clase.

### Reglas de Declaración para Archivos de Código
Antes de adentrarnos en la declaración de clases, demos un rápido repaso de las reglas asociadas con la declaración, la importación de sentencias y paquetes en un archivo fuente.
- Solo puede haber una clase ***public*** por archivo fuente.
- Los comentarios pueden aparecer al principio o al final de cualquier línea de código en el archivo fuente.
- Si hay una clase ***public*** en el archivo fuente, el nombre del archivo debe ser el mismo que de la clase ***public***.
- Si la clase es parte de un paquete, la sentencia del paquete debe ser la primera linea del código fuente, antes incluso que de cualquier ***import***.
- Si hay sentencias ***import***, estas deben ir entre la sentencia del paquete y la declaración de la clase. Si no hay declaración de paquete, las primeras lineas de código deben ser las sentencias ***import***. Si no hay sentencias ***package*** o ***import***, la declaración de la clase debe ser la primera linea del código.
- Las sentecias ***import*** y ***package*** aplican para todas clases dentro de un archivo de código. Es decir no pueden existir multiples declaraciones de clases en un unico archivo de código y que tengan diferentes paquetes o usar usar distintos ***imports**.
- Un archivo de código puede tener más de una clase no ***public***.
- Los archivos que no tengan una clase ***public*** pueden ser nombras con un nombre que no coincida con ninguna de las clases declaradas dentro de ella.

### Declaración de Clases y Modificadores
El siguiente código es una declaración de una clase cualquiera:
```java
class AnyClass {}
```
Este código compilara perfectamente, pero tambien se pueden agregar modificadores antes de la declaración de la clase.
Los modificadores tienen 2 categorias:
- **Modificadores de Acceso:** *public*, *protected* y *private*.
- **Modificadores de no acceso:** *strictfp*, *final* y *abstract*.

A continuación veremos los modificadores de acceso y aprenderemos como permitir o restringir el acceso a las clases que creemos. El control de acceso en Java es un poco complicado ya que **hay 4 niveles de acceso pero solo 3 modificadores**. El cuarto nivel de acceso llamado ***default*** o ***package access*** es el que se usa cuando no utilizamos ninguno de los otros 3 modificadores. En otras palabras, ***toda clase, método, variable que declaremos tienen un control de acceso explicitamente uno (public, protected o private) o no (default)***.

Sin embargo una *clase* solo puede ser declarada como *public* o *default*, los otros 2 modificadores no marcan ninguna diferencia para una clase.

### Acceso a una clase
Cuando decimos que el codigo de una clase (Clase A) tiene acceso a otra clase (Clase B), quiere decir que A puede hacer una de 3 tres cosas:
- Crea una instancia de la clase B.
- Hereda o extiende de la clase B.
- Acceder a ciertos métodos y variables dentro de la clase B, dependiendo del nivel de acceso de estos.

En la practica, *acceso* significa *visibilidad*. Si la clase A no puede ver a la clase B, el nivel de acceso de los métodos y variables de la clase B no inportan ya que la clase A no tiene manera de acceder a ellos.

### Acceso por Defecto (Default access)
Una clase con acceso por defecto, no tiene un modificador que preceda a su declaración. Pensemos en el acceso por defecto como un acceso a nivel de paquete (*package*), porque una clase con *default access* solo puede ser vista por otras clases que esten dentro del mismo paquete. Por ejemplo si la clase A y B estan en distintos paquetes y la clase A tiene *default access*, la clase B no podra crear instancias de la clase A, ni declarar o retornar una variable que sea de un tipo de la clase A. De hecho la clase B tiene que pretender que la clase A no existe. Veamos el siguiente código de ejemplo:

Tenemos una clase con *default access* dentro de un paquete llamado *cert*
```java
package cert;
class Beverage { }
```
Y una segunda clase dentro de otro paquete que hereda la clase anterior.
```java
package exam.stuff;
import cert.Beverage;
class Tea extends Beverage { }
```
Como podemos ver ambas clases estan en distintos paquetes. La sentencia *import* arriba de la clase *Tea* intenta importar la clase Beverage. La clase Beverage compilará correctamente, pero cuando se intente compilar la clase Tea obtendremos un error de compilación como el siguiente:
```java
Cant access class cert.Beverage. Class or interface must be
public, in same package, or an accessible member class.
import cert.Beverage;
```
La clase *Tea* no compilara porque intenta heredar de una clase que se encuentra en otro paquete y que tiene *access default*. Para que funciones podemos poner ambas clases dentro de un mismo paquete o declarar la clase *Beverage*
como *public*, como lo veremos a continuación.

### Acceso Público (*public*)
Una clase declarada como *public* le da acceso a todas las clases de todos los paquetes. No olvidar que si queremos usar esta clase *public* en otro paquete debemos realizar la importación de esta a través de la sentencia *import*.

Si en el ejemplo anterior marcamos la clase *Beverage* como *public*
```java
package cert;
public class Beverage { }
```
Al hacer este cambio, ambas clases *Beverage* y *Tea* compilaran correctamente.

### Modificadores de No Acceso (*Nonaccess Modifiers*)
Podemos modificar una clase con los modificadores *final*, *abstract* y *strictfp*. Estos modificadores son adicionales a los modificadores de acceso por lo que se podria marcar una clase como *public* y *final*. Pero no podemos usar ambas *final* y *abstract*, a diferencia de que sí se puede usar *strictfp* junto con *final*.

No necesitamos saber como es que trabaja *strictfp*, ya que con enfocaremos solo en modificar una clase con *final* o *abstract*. Para el examen solo es necesario saber que *strictfp* es una palabra reservada y que puede ser usada para modificar una clase o un método, pero jamás una variable.

### Clases Final (*final class*)
Cuando marcamos una clase como *final* quiere decir que no puede ser heredada. En otras palabras, ninguna otra clase puede heredar o extender de una clase *final*, cualquier intento de esto resultará en un error de compilación.

Podemos marcar una clase como *final* si y solo sí necesitamos la absoluta garantía de que ninguno de los métodos dentro de esa clase puedan ser sobreescritos.

### Clases Abstractas (*abstract class*)
















