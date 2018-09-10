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
        return this.size;
    }

    public void setSize(int size) {
        this.size = size;
    }

}
```

## 2. Herencia
___

## 3. Polimorfismo
___

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

