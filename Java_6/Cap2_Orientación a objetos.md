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



## 4. Sobreescritura y Sobrecarga
___

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

