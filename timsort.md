## Timsort

Suponiendo la lista
`[5, 3, 1, 4, 2, 8, 7, 6]`

### Divide en runs pequeños

```
[5, 3, 1, 4]     [2, 8, 7, 6]
   run 1            run 2
```

### Ordena cada run con Insertion Sort (= inserción directa)

> Nota: método de insercion directa = comparacion de elementos con parte izquierda

Ordena [5, 3, 1, 4]:

```
5 3 ->      [3, 5]
3 5 1 ->    [1, 3, 5]
1 3 5 4 ->  [1, 3, 4, 5]
```

Ordena [2, 8, 7, 6]

```
2 8 ->      [2, 8]
2 8 7 ->    [2, 7, 8]
2 7 8 6 ->  [2, 6, 7, 8]
```

### Merge de los runs ordenados (como en Merge Sort)

Teniendo los runs ordenados `[1, 3, 4, 5]` y `[2, 6, 7, 8]`
```
Compara 1 y 2 -> 1              [1]
Compara 3 y 2 -> 2              [1, 2]
Compara 3 y 6 -> 3              [1, 2, 3]
Compara 4 y 6 -> 4              [1, 2, 3, 4]
Compara 5 y 6 -> 5              [1, 2, 3, 4, 5]
Luego quedan 6, 7, 8 -> añadir al final         [1, 2, 3, 4, 5] +  [6, 7, 8]
```

### Resultado

```
[1, 2, 3, 4, 5, 6, 7, 8]
```
