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
Una clase abstracta no puede ser instanciada, solo puede ser heredada.

Podriamos usar clases abstractas, cuando querramos englobar objetos de distintos tipos y hacer uso del polimorfismo.

Por ejemplo, podriamos tener una clase abstract *Figura* que define el método *area()*, notemos que figura es una generalización y que no tendria sentido definir el area de una figura. Sin embargo podremos heredarla en una clase como *Cuadrado* o *Circulo* donde sí podriamos implementar el método definido en la superclase abstracta *Figura*

```java
// Clase abstracta Figura
public abstract class Figura {
    protected double x;
    protected double y;

    public Figura (double x, double y) {
        this.x = y;
        this.y = y;
    }

    public abstract double area();
}

public class Circulo extends Figura {
    private double radio;

    public Circulo (double x, double y, double radio) {
        super(x,y);
        this.radio = radio;
    }

    public double area() {
        return Math.PI*radio*radio;
    }
}

public class Cuadrado extends Figura {
    private double lado;

    public Circulo (double x, double y, double lado) {
        super(x,y);
        this.lado = lado;
    }

    public double area() {
        return lado*lado;
    }
}
```

## 4. Declaración de Interfaces
___
Una interfaz en palabras simples, *es una clase completamente abstracta, es decir una clase sin implementación*. 

Cuando creamos una *interfaz*, definimos un contrato de *que es lo que hará una clase, más no de como lo hará*

### Caracteristicas de una interfaz

- Mientras una clase abstracta puede definir tanto métodos abstractos y no abstractos, una interfaz solo puede definir métodos implícitamente públicos y abstractos.

- Todas las variables definidas en una interfaz, deben ser *public*, *static* y *final*, es decir una interfaz solo puede declarar ***Constantes***.
- Una interfaz puede extender o heredar de una o más interfaces. Pero jamás de una clase.
- Una interfaz no puede implementar otra interfaz o clase.
- Deben ser declaradas usando la palabra reservada *interface*.
- Si una clase implementa una interfaz, esta debe implementar todos los métodos definidos en la interfaz.

## 5. Declaración de Miembros de Clase.
___

Los métodos y variables son tambien llamados miembros. Podemos modificar los miembros con modificadores de acceso y de no acceso o de una combinación de ambos.

Se puede acceder a un método o variable de una clase haciendo uso del operador (**.**).

## Modificadores de Acceso

### Miembros Públicos
Cuando un miembro es declarado como *public*, significa que todas las clases independientemente del paquete al que pertenezcan, tienen acceso a este miembro. Para una subclase si un miembro de su superclase es declarada como *public* , la subclase puede heredar este miembro independientemente del paquete de ambas clases.

Formas de acceso:
- Invocando un miembro declarado en la misma clase.
- Invocando un miembreo usando una referencia de la clase.
- Invocando un método heredado.

### Miembros Privados
Los miembros declarados como *private* no pueden ser accesidos por otra clase más que en la que fue declarada.

Formas de acceso:
- Invocando un miembro declarado en la misma clase.
  
### Protected y Default
Los modificadores *protected* y *default* son muy parecidos. Pero hay una diferencia muy significativa. Un miembro declarado como *default* puede ser accesido solo si la clase pertenece al mismo paquete, mientras que un miembro declarado como *protected* solo puede ser accesido por medio de *herencia* a través de una subclase, sin importar el paquete al que pertenesca ó si la clase pertenece al mismo paquete.

### Tabla de visibilidad

|**Visibilidad**|**public**|**protected**|**default**|**private**|
|---------------|----------|-------------|-----------|-----------|
|Desde la misma clase|si|si|si|si|
|Desde la cualquier clase en el mismo paquete|si|si|si|no|
|Desde una subclase en el mismo paquete|si|si|si|no|
|Desde una subclase en otro paquete|si|solo por herencia|no|no|
|Desde una clase en otro paquete|si|no|no|no|

## Modificadores de no-acceso aplicados a métodos
### Métodos *final*
El modificador *final* previene que un método sea anulado o sobreescrito en una subclase. Esta restricción de sobreescritura provee consistencia y seguridad, pero se deben usar con mucho cuidado.

Ejemplo se tiene la siguiente clase:
```java
class SuperClass{
    // final method
    public final void showSample() {
        System.out.println("One thing.");
    }
}
```
Heredamos en una subclase y tratamos de sobreescribir el m1étodo *showSample()*
```java
class SubClass extends SuperClass{
    public void showSample() { 
        // Try to override the final
        // superclass method
        System.out.println("Another thing.");
    }
}
```
Al intentar compilar tendremos un error de compilación como el siguiente:
```java
%javac FinalTest.java
FinalTest.java:5: The method void showSample() declared in class
SubClass cannot override the final method of the same signature
declared in class SuperClass.
Final methods cannot be overridden.
public void showSample() { }
1 error
```

### Argumentos *final*
Los argumentos de un método, son las variables declaradas que aparecen entre los paréntesis en la definición de un método.
```java
public Record getRecord(int fileNumber, int recNumber) {}
```
Los argumentos son esencialmente lo mismo que las variables locales y se aplicaran las mismas reglas que estas. Esto quiere decir que los argumentos de un método pueden tener el modificador *final*.
```java
public Record getRecord(int fileNumber, final int recordNumber) {}
```
En el ejemplo anterior el argumento *recordNumber* esta declarada como *final*, lo que indica que no puede ser modificada dentro del método. En otras palabras esto quiere decir que el argumento *final* debe mantener el mismo valor que tiene cuando el método es invocado y se pasa un parámetro a este argumento.

### Métodos Abstract (*abstract methods*)
Un método abstracto es un método que puede ser declarado pero no implementado. Un método se declara como abstracto, cuando se quiere forzar la implementación en una subclase que la hereda.

### Métodos Sincronizados (*Synchronized Methods*)
La palabra reservada *synchronized* indica que un método solo puede ser accesido por un hilo a la vez. *synchronized* solo es aplicable a métodos. Su declaración es como la siguiente:
```java
public synchronized Record retrieveUserInfo(int id) { }
```
### Métodos Nativos (*Native methods*)
El modificador *native* indica que un método es implementado en una plataforma de código dependiente. Se vera su funcionamiento más adelante. Este modificador solo puede ser aplicado a métodos y al igual que un método abstracto su declaración terminará en (;) y no en llaves ({}).

### Métodos con Argumentos Variables
Java permite crear métodos que pueden tener un número variable de argumentos. Esta capacidad es referenciada como: 
*"variable-length argument lists," "variable arguments," "var-args," "varargs"* y en este libro la llamaremos *"var-args"*
- **argumentos**: Es lo que se especifica entre paréntesis cuando se invoca un método.
```java
doStuff("a", 2); // invocando a doStuff, a & 2 son argumentos
```
- **parámetro**: Es lo que indica que debe recibir un método cuando este es invocado.
```java
void doStuff(String s, int a) { } 
// Se espera 2 parámetros 1 String y 1 int.
```
Las reglas para declarar argumentos variables (*var-args*) son:

- **Tipo de var-arg**: Cuando se declaran parámetros *var-arg* se debe especificar el tipo de argumento que este parámetro puede recibir cuando el método sea invocado. (Pueden ser de tipo primitivo o un objeto).
- **Sintaxis Básica**: Al declarar un método con parámetros *var-arg*, al tipo de argumento le debe preceder una *ellipsis* (...) seguida de un espacio y el nombre del arreglo que contendrá los parámetros recibidos.
- **Otros parámetros**: Es completamente válido tener otros parámetros en un método que use *var-arg*.
- **Límite de var-arg**: No puede haber más de un argumento *var-arg* en un método, y este debe ser el último en declararse.

Ejemplos:
```java
// Válido:
void doStuff(int... x) { } // Se espera de 0 a muchos parámetros de tipo int
void doStuff2(char c, int... x) { } // Se espera un parámetro tipo char y 0 o más parámetros tipo int
void doStuff3(Animal... animal) { } // Se espera ninguno o muchos objetos de clase Animal.

// Inválido
void doStuff4(int x...) { } // Error de sintaxis
void doStuff5(int... x, char... y) { } // Demasiados argumentos var-arg
void doStuff6(String... s, byte b) { } // El argumento var-arg debe ser el último en declararse
```

### Declaración del Constructor
En Java los objetos son construidos, cada vez que se crea un nuevo objeto de una clase es invocado un método constructor. Cada clase tiene un método constructor, si no se crea explicitamente, el compilador construye uno implícitamente en nuestro lugar. En el cap 2,veremos en detalle las reglas que conciernen a los constructores.

Su definición es la siguiente:
```java
class Foo {
    protected Foo() { } // Este es el constructor de Foo
    protected void Foo() { } // Esta mal llamada, pero es un método valido
}
```
- No debe retornar ningun tipo.
- Debe tener el mismo nombre que la clase.
- Un constructor puede tener modificadores de acceso y argumentos incluso argumentos *var-arg*.
- No puede ser definido como *static*, *final* o *abstract*.
```java
class Foo2 {
    // legal constructors
    Foo2() { }
    private Foo2(byte b) { }
    Foo2(int x) { }
    Foo2(int x, int... y) { }
    // illegal constructors
    void Foo2() { } // Es un método y no un constructor
    Foo() { } // No es un método ni un constructor
    Foo2(short s); // Parece un método abstracto.
    static Foo2(float f) { } // No puede ser statico
    final Foo2(long x) { } // No puede ser final
    abstract Foo2(char c) { } // No puede ser abstracto
    Foo2(int... x, int t) { } // Error de sintaxis en la declaracion del argumento var-arg
}
```
### Declaración de Varibles
Hay 2 tipos de variables en Java
- **Primitivas**: Una variable puede ser una de 8 tipos: *char, boolean, byte, short, int, long, double o float*. Cuando una variable primitiva es declarada su tipo no podrá ser cambiado, sin embargo en muchos casos su valor podrá cambiar.

- **Variables de referencia**: Una variable de referencia se usa para acceder o hacer referencia a un Objeto. Una variable de referencia es declarada para ser de un tipo específico y no podra ser cambiada.

### Declaración de tipos y rangos primitivos
Los 6 tipos de números primitivos en Java estan formados por un cierto número de bytes de 8 bits y pueden ser *positivos* y *negativos*.

El bit más a la izquierda es el más relevante e indica el signo, si es 1 es *negativo* y si es 0 es *positivo*, los otros bits representan el valor.

|**Tipos**|**Bits**|**Bytes**|**Valor Mínimo**|**Valor Máximo**|
|---------------|----------|-------------|-----------|-----------|
|byte|8|1|-2<sup>7</sup>|2<sup>7</sup>-1|
|short|16|2|-2<sup>15</sup>|2<sup>15</sup>-1|
|int|32|si|4|-2<sup>31</sup>|2<sup>31</sup>-1|
|long|64|8|-2<sup>63</sup>|2<sup>63</sup>-1|
|float|32|4|n/a|n/a|
|double|64|8|n/a|n/a|

### Declarando Variables de Referencia
Las variables de referenca pueden ser declaradas como variables estáticas, instancias, parámetros de métodos o variables locales. Se pueden declarar más de una variables del mismo tipo en una sola linea. Se discutirá mas en detalle en el capítulo 3.

### Variables de Instancia
Las variables de instancia son declaradas dentro de una clase, pero fuera de cualquier método y son inicializadas solo cuando la clase es instanciada. Las variables de instancia son los campos o atributos unicos que tendrán los objetos.

- Las variables de instancia pueden ser declaradas con cualquier de los 4 modificadores de acceso.
- Pueden ser declaradas como *final* y *trascient*.
- No pueden ser declarados como *abstract, synchronized, strictfp o native*.

### Variables Locales
Las variables locales son variables declaradas dentro de un método. Esto quiere decir que no necesitan ser inicializadas dentro del método pero sí, declaradas junto con el.

- Una variable local debe ser inicializada antes de poder ser usada.
- Una variable local no puede ser referenciada en ningun lugar del código, mas que en el método en el cual fue declarado.

### Declaración de arreglos
En Java los arreglos son objetos que almacenar multiples variables de un mismo tipo ya sean de un tipo primitivo o de un objeto.

```java
// Arreglo de variables de tipo primitivo
int[] key // Estándar con los corchetes antes del nombre del arreglo
int key[] // Válido pero no recomendable
```

Podemos declarar arreglos multidimensionales que vendrian a ser arreglos de arreglos.

```java
String[][][] occupantName; // Arreglo tridimensional
String[] manager[] managerName; // Arreglo bidimensional
String[][] managerName; // Arreglo bidimensional
```

- Es incorrecto incluir la longitud de un arreglo en su declaración.

### Variables *final*
Declarar una variabla como *final* hace que sea imposible reiniciar la variable una vez que ha sido inicializada con un valor explícito.

### Declarando Enums
Un enum, también llamado enumeración o tipo enumerado es un tipo de dato definido por el usuario que solo puede tomar como valores los definidos en una lista.

*...Conseguir información mas relevante y explícita sobre enums*






