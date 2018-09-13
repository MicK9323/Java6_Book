# CAPITULO 2: Orientación a objetos.

## 1. Encapsulación
___
La habilidad de hacer cambios en la implementación del código sin romper el código que pueden estar usando otros es un beneficio clave de la encapsulación.

Si queremos mantenibilidad, flexibilidad y extensibilidad, el diseño de nuestro código debe incluir encapsulación. Como lo hacemos?
- Manteniendo las variables de instancia protegidas por un modificador de acceso (casi siempre *private*).
- Hacer métodos de acceso público y forzar su llamada para emplearlos en lugar de acceder a la variable directamente.
- Para estos métodos usar la convención de nombres de JavaBeans
*set\<someProperty>* y *get\<someProperty>*.

```java
public class Box {

    private int size;

    public int getSize() {
        return this.size; // Devuelve el valor de size
    }

    public void setSize(int size) {
        this.size = size; // Cambia el valor de size
    }

}
```

## 2. Herencia
___
La *herencia* esta presente en todo Java, se podria decir que es casi imposible desarrollar cualquier aplicación en Java sin hacer uso de la *herencia*.

Comenzaremos viendo el uso del operador *instanceOf* (más detallado en el capítulo 4), por ahora solo importa saber que *instanceOf* devolverá *true* si la variable que se esta probando es del mismo tipo con el que esta siendo comparada.

```java
class Test {
    public static void main(String [] args) {
    Test t1 = new Test();
    Test t2 = new Test();

    if (!t1.equals(t2))
        System.out.println("they're not equal");

    if (t1 instanceof Object)
        System.out.println("t1's an Object");
    }

    // Retornará:
    // they're not equal
    // t1's an Object
}
```
Las 2 razones más comunes para usar herencia son:
- **Implementar la reutilización de código.**

  Comenzemos con la reutilización de código, un enfoque común que consiste en crear versiones bastante genéricas de una clase con la intención de crear subclases mas especializadas que hereden de el.

- **Usar el polimorfismo.**
  Relacionado con el uso de la herencia, permite acceder a las clases poliformicamente (*una capacidad proveida por interfaces*). Una ventaja del polimorfismo (*muchas formas*) es que se puede crear muchas subclases de una superclase como si fuera una superclase.
 
### Relaciones IS-A y HAS-A
### IS-A
En la orientación a objetos la relación IS-A está basada en la herencia de clases y la implementación de interfaces. IS-A es una forma de decir "*Esta cosa es de este tipo*". Por ejemplo: Subaru IS-A Car, Zanahoria IS-A Vegetal.

Las relaciones IS-A en java se expresan usando *extends* (para herencia de clases) e *implements* (para implementación de interfaces).

```java
public class Vehicle { ... }
public class Car extends Vehicle { ... }
public class Subaru extends Car { ... }
```
Del código anterior también podemos decir que la expresión *Subaru instanceOf Vehicle* retorna *true*, aun si *Subaru* no hereda directamente de *Vehicle* sino de una subclase de ella.

### HAS-A
Las relaciones HAS-A se basan más en el uso de algo que en la herencia en si. En otras palabras class A HAS-A B si en el código de la clase A existe una referencia a una instancia de la clase B.

```java
public class Animal { }

public class Horse extends Animal {
    // Instancia de un objeto de la clase Halter
    private Halter myHalter;
}
```


## 3. Polimorfismo
___
Se utiliza este término en POO para referir a la *propiedad por la que es posible enviar mensajes sintacticamente iguales a objetos de distintos tipos.*

Como vemos es un concepto muy avanzado y es muy util si queremos jerarquizar y dar un patrón de comportamiento común a una serie de objetos que heredan de a misma clase.

Cualquier objeto de Java que pase más de una prueba IS-A puede ser considerada polimorfica. Aparte de los objetos de tipo *Object*, todos los objetos en Java son polimorficos ya que pasan la prueba IS-A para su mismo tipo y para la clase *Object*. Recordemos que la unica forma de acceder a un objeto es a través de una varible de referencia.

Recordemos que:

- Una variable de referencia puede ser de un solo tipo y una vez declarada este no puede cambiar.
- Una referencia es una variable que puede ser asignada a otros objetos (A no ser que la referencia se haya declarado como *final*).
- Eltipo de variable de una referencia indica que métodos pueden ser invocados en el objeto que la variable hace referencia.
- Una variable de referencia puede hacer referencia  cualquier objeto del mismo tipo al que es declarado o a cualquier subtipo del objeto con el que ha sido declarada.
- Una variable de referencia puede ser declarada como un tipo de una clase o de una interfaz. Si la variable es declarada como una interfaz, puede hacer referencia a cualquier objeto de cualquier clase que implemente la interfaz.
- Una clase no puede heredar de más de una clase.

## 4. Sobreescritura y Sobrecarga
___
### Sobreescribir un método
Siempre que se tenga una clase que herede un método de una superclase, tenemos las oportunidad de sobreescribir este método (a menos que el método haya sido declarado como *final* en la superclase). Esto nos permite definir comportamientos específicos para una subclase en particular.

Ejemplo:

```java
public class Animal {
    public void eat() {
        System.out.println("Generic Animal Eating Generically");
    }
}
class Horse extends Animal {
    public void eat() {
        System.out.println("Horse eating hay, oats, "
                            + "and horse treats");
    }
}
```

Recordemos que:

- Los métodos abstractos que se heredan de una superclase, deben ser implementados en las subclases (a no ser que la subclase tambien sea abstracta).
- Los métodos abstractos deben ser implementados por las subclases, pero es mejor decir que las subclases **sobreescriben** los métodos abstractos de una superclase.
- Entonces se puede decir que: *Los métodos abstractos, son métodos que estamos forzados a sobreescribir*.

Tenemos el siguiente código:

```java
public class TestAnimals {
    public static void main (String [] args) {
        Animal a = new Animal();
        Animal b = new Horse(); //Animal ref, but a Horse object
        a.eat(); // Runs the Animal version of eat()
        b.eat(); // Runs the Horse version of eat()
    }
}

class Animal {
    public void eat() {
        System.out.println("Generic Animal Eating Generically");
    }
}

class Horse extends Animal {
    public void eat() {
            System.out.println("Horse eating hay, oats, "
                                + "and horse treats");
        }

    public void buck() { }
}
```

En el código anterior, la clase *TestAnimals* usa una referencia de la clase *Animal* para llamar a el método *eat()* del objeto de tipo *Horse*. Cabe señalar que en la definición anterior, el compilador solo reconocerá los métodos de la clase *Animal* cuando este es usado como referencia. En el código siguiente se muestra una forma inválida de definición.

```java
    Animal c = new Horse();
    c.buck(); // Can't invoke buck();
    // Animal class doesn't have that method
```

Se intenta llamar a el método *buck()* definido en la clase *Horse* pero esta al usar una referencia a su superclase *Animal* no reconoce este método y el código no compilará.

Las reglas para la sobreescritura de métodos son los siguientes:
- La lista de argumentos debe coincidir con los argumentos del método a sobreescribir. Si no coinciden se está sobrecargando el método y puede que esto no sea lo que estes intentando hacer.
- El tipo de retorno del método debe ser del mismo tipo o un subtipo de retorno que del método que se esta sobreescribiendo.
- El nivel de acceso no puede ser más restrictivo que del método original.
- El nivel de acceso no puede ser menos restrictivo que del método original.
- Los métodos de instancia pueden ser sobreescritos solo si son heredados por una subclase.
    - Una subclase que esté en el mismo paquete que su superclase podrá sobreescribir podrá sobreescribir cualquier método de su superclase que no este definida como *private* o *final*.
    - Una subclase que este fuera del paquete de su superclase, solo podra sobreescribir los métodos que no esten definidos como *final* y sean de acceso *public* o *protected* (Dado que los métodos *protected* son heredados por las subclases).
- Un método sobreescrito puede ejecutar cualquier excepción no verificada (*runtime*), independientemente de si hay una excepción declarada en el método que se ha reemplazado.
- Un método sobreescrito no puede ejecutar ninguna excepción nueva o mas amplia que la declarada en el método reemplazado. Por ejemplo un método declara un *FileNotFoundException* no puede ser reemplazado por un *SQLException*, *Exception* o cualquier otra excepción (*non-runtime*) a no se que sea una subclase de *FileNotFoundException*
- No se puede sobreescribir un método declarado como *final* o *static*.
- Si un método no puede ser heredado no puede ser sobrescrito.

### Invocar la versión de superclase de un método sobreescrito.
Si se quiere hacer uso del método original declarado en la superclase, se pueder hacer mediante el uso de la pabra reservada *super*. Observe el ejemplo.

```java
public class Animal {
    public void eat() { }
    public void printYourself() {
    // Useful printing code goes here
    }
}
class Horse extends Animal {
    public void printYourself() {
    // Take advantage of Animal code, then add some more
    super.printYourself(); // Invoke the superclass
    // (Animal) code
    // Then do Horse-specific
    // print work here
    }
}
```

|Sobreescritura inválida|Problema|
|-----------------------|--------|
|private void eat() { }|Nivel de acceso muy restrictivo.|
|public void eat() throws IOException { }|Declara una excepción comprobada no declarada en la versión de superclase.
|public void eat(String food) { }|Es una sobrescarga, más no una sobreescritura ya que los argumentos han cambiado.
|public String eat() { }|No es una sobreescritura porque cambia el tipo de retorno y no es una sobrecarga porque no ha cambiado el número de argumentos.


## 5. Casting
___

## 6. Implementación de Interfaces
___

## 7. Tipos de Retorno
___

## 8. Constructores e Instancias
___

## 9. Estáticos
___

