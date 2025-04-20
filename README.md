# Actividad 9 - Ordenación y búsqueda


## Ordenación de estructuras lineales

### 1. Inserción directa

**Ejercicio 75**

El método de **inserción directa** consiste en **ir insertando cada elemento** de un arreglo en la **parte izquierda**, que **ya está ordenada**, desplazando los elementos mayores si es necesario hasta encontrar su posición correcta

Por ejemplo:

```
[20, 42, 22, 60, 10, 100]
      ^ se compara con la parte izquierda (20)
      20 < 42 con lo cual lo dejamos como está

[20, 42, 22, 60, 10, 100]
          ^ se compara con la parte izquierda (42)
          42 > 22 con lo cual los intercambiamos

[20, 22, 42, 60, 10, 100]
      ^ se compara con la parte izquierda (20)
        20 < 22 con lo cual lo dejamos como está

[20, 22, 42, 60, 10, 100]
              ^ pasa directamente a 60 (porque 42 está ordenado) y se compara con la parte izquierda (42)
                42 < 60 con lo cual lo dejamos como está

compara el 10 por cada uno de los números a su izquierda
```
... así hasta obtener ```[10, 20, 22, 42, 60, 100]```

**Ejercicio 76**

La complejidad temporal en el **peor caso** del **método de inserción directa** es **O (n^2)**, donde **n** es el **número de elementos**, ya que en el peor caso (elementos en **orden inverso**) **cada elemento** debe **compararse y moverse** a lo largo de toda la parte ordenada.

Un ejemplo de **peor caso** es:

```
[100, 60, 42, 22, 20, 10]
       ^ compara y mueve 1 vez

[60, 100, 42, 22, 20, 10]
           ^ compara y mueve 2 veces

[42, 60, 100, 22, 20, 10]
               ^ compara y mueve 3 veces

[22, 42, 60, 100, 20, 10]
                   ^ compara y mueve 4 veces

[20, 22, 42, 60, 100, 10]
                       ^ compara y mueve 5 veces

[10, 20, 22, 42, 60, 100]
```

Como vemos, **cada elemento** debe ser movido **hasta el principio del arreglo**, con lo cual realiza el **maximo número de comparaciones y movimientos posibles**.

**Ejercicio 77**

El **método de inserción directa** se utiliza principalmente :

- Cuando **se tienen pocos elementos**
- Cuando el arreglo **está casi ordenado**

ya que en estos casos **puede ser más eficiente** que otros **algoritmos más complejos**

**Ejercicio 78**

> Libro: "Data structures and algorithms in Java. Pearson" con autor "Weiss, M." (2012)

Enlace [preview del libro](https://archive.org/details/datastructuresal0000weis_f2o8/page/248/mode/2up?q=sorting) | Enlace [captura de pantalla](https://github.com/user-attachments/assets/7a5d78e7-584c-400b-9ce8-9d94c890e11d) (páginas **248 - 249**)

```
public static <AnyType extends Comparable<? super AnyType>>
void insertionSort (AnyType [] a) {
    int j;

    for (int p = 1; p < a.length; p++) {
        AnyType tmp = a[p];
        for (j = p; j > 0 && tmp.compareTo(a[j-1]) < 0; j--)
            a[j] = a[j-1];
        a[j] = tmp;
    }
}
```

**Explicación** Este código de **inserción directa** (insertion sort):
- Recorre el arreglo desde la segunda posición `int p = 1` y
- **para cada elemento** `p < a.length; p ++`
- **compara hacia la izquierda**, siempre que no haya **llegado al primer elemento**: `j > 0`
- y **mientras el elemento actual** `tmp` sea **menor** que el anterior: `tmp.compareTo(a[j-1]) < 0`
- **desplaza** el elemento **mayor** una posición a la **derecha**: `a[j] = a[j-1];`
- finalmente, inserta el **elemento actual** en su **posición correcta** (después de desplazar los mayores): `a[j] = tmp;`


### 2. Mergesort

**Ejercicio 79**

**Mergesort** es un algoritmo de ordenación basado en la técnica **"divide y vencerás"**. Su funcionamiento consiste en:

- **Dividir** la lista en **dos mitades**.
- **Ordenar recursivamente** cada mitad.
- **Mezclar** (= merge / fusionar) las dos mitades ordenadas en **una sola lista ordenada** (comparando cada elemento de la lista izquierda con los de la derecha)

[Video simulación](https://www.youtube.com/watch?v=5Z9dn2WTg9o)

Volviendo al ejemplo de la lista usada anteriormente

`[100, 60, 42, 22, 20, 10]`

```
[100, 60, 42, 22, 20, 10]

[100, 60, 42] [22, 20, 10] // Divide en 2 mitades

[42, 60, 100] [10, 20, 22] // Ordena cada una por separado:

Compara y añade a lista final

               []
42 > 10 ? ->   [10],
42 > 20 ? ->   [10, 20]
42 > 22 ? ->   [10, 20, 22]

Ya no quedan más en la derecha para comparar, así que añadimos la otra lista entera (ya estæ ordenadao):

= [10, 20, 22]  + [42, 60, 100] = [10, 20, 22, 42, 60, 100]
```

**Ejercicio 80**

La **complejidad temporal** en el **peor caso** de **Mergesort** es O(n log n), donde n es el número de elementos.
Esto se debe a que el algoritmo divide el arreglo **en mitades** (**log n** divisiones) y en **cada nivel de recursión** fusiona **todos** los elementos (n operaciones)


**Ejercicio 81**

Enlace [preview del libro](https://archive.org/details/datastructuresal0000weis_f2o8/page/258/mode/2up?q=sorting) | Enlace [captura de pantalla](https://github.com/user-attachments/assets/8ed04922-48bd-4d63-aad9-71da02413e5c) (páginas **260 - 261**)


### 3. Timsort

**Ejercicio 82**

> a) Run

Subsecuencia consecutiva ya ordenada (creciente o decreciente) en la lista.

> b) Minrun

Tamaño mínimo de run que Timsort usa para garantizar eficiencia (entre 32 y 64).

> c) Inserción binaria

Técnica que encuentra la **posición correcta** usando **comparaciones binarias**. Por ejemplo:

```
[10, 20, 30, 40, _, 60] // queremos insertar 35
                ^ posición a insertar

Búsqueda binaria:
1. Compara con medio (20): 35 > 20
2. Compara con (40): 35 < 40
3. Posición correcta encontrada: entre 30 y 40

[10, 20, 30, 35, 40, 60] // resultado final
```

**Más eficiente** que comparar **elemento por elemento**.

> d) Ejemplo de funcionamiento de Timsort:

Ver [explicación aquí](timsort.md)


> e) Quien inventó el algoritmo

**Tim Peters** en **2002** para integrarlo en el lenguaje de programación **Python**

> f) Qué complejidad tiene

[Articulo interesante](https://medium.com/@rylanbauermeister/understanding-timsort-191c758a42f3) (tiene unaa tabla con la complejidad en varios casos para diferentes algoritmos)

La complejidad de este algoritmo es en el **mejor** caso es **O(n)** y en los casos **promedio** y **peor** tiene complejidad **O(n log n)**
