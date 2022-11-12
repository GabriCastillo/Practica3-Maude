# Practica3-Maude

## Ejercicio 1.1: La panadería de Lamport

### 1 - Analiza la confluencia, terminación y coherencia del sistema definido.

**Es confluente**, puesto que en todo momento solo hay una ecuación en la que un input puede hacer matching. De forma que solo hay un posible camino de reducción y por tanto no puede ser no-confluente. 

**No es terminante**, ya que el protocolo logra la exclusión mutua entre procesos, y por lo tanto no hay estados de bloqueo, considerados finales. La siguiente ejecución muestra un contraejemplo:

```
Maude> rew initial(5) .
rewrite in Bakery : initial(5) .
Debug(1)> q
Bye.
```

Como podemos ver el estado generado no termina y por tanto no es terminante. 

**Es coherente**, dado que una vez creado el estado inicial, todos los estados se encuentran en forma irreducible. De forma que no se intercalan pasos de rescriturar con reducción, y por tanto no puede ser no-coherente.  

### 2 - ¿Es el espacio de búsqueda alcanzable a partir de estados definidos con el operador initial finito? Utiliza el comando search para comprobar la exclusión mutua del sistema con 5 procesos.

**El espacio de búqueda es infinito**. Dado que cada vez que un cliente (_BProcess_) hace un ciclo---Entendiendo hacer un ciclo como que pasas de sleep a wait, de wait a crit y de crit de nuevo a sleep---el número del tícket expendido por el dispensador (_last_) ha incrementado en al menos 1, y dado que no es terminante; se pueden generar infinitos estados en lo que único que cambia es el número del ticket expendido, que puede tomar como valor todo número naturarl (_Nat_).    

```
Maude> search [1] initial(5) =>* [[< O:Nat : BProcess | mode: crit, number: P:Nat > < O':Nat : BProcess | mode: crit, number: P':Nat > C:Configuration ]] s.t. O:Nat =/= O':Nat .
search [1] in Bakery : initial(5) =>* [[C < O : BProcess | mode: crit, number: P > < O':Nat : BProcess | mode: crit,number: P':Nat >]] such that O =/= O':Nat = true .
Debug(1)> q
Bye.
```

Como podemos ver no podemos demostrarlo con el comando search, ya que al ser el espacio de búqueda infinito, es imposible explorar todo el especio de búqueda. Lo único que podemos decir es que no lo ha encontrado en lo que ha explorado. 

### 3 - Utiliza el comando search para comprobar si hay estados de bloqueo.

```
Maude> search [1] initial(5) =>! S:GBState .
search [1] in Bakery : initial(5) =>! S:GBState .
Debug(1)> q
Bye.
```

omo podemos ver no podemos demostrarlo con el comando search, ya que al ser el espacio de búqueda infinito, es imposible explorar todo el especio de búqueda. Lo único que podemos decir es que no lo ha encontrado en lo que ha explorado. 

## Ejercicio 1.2: ABSTRACT-BAKERY

### 4 - Justifica la validez de la abstracción (protección de los booleanos, confluencia y terminación de la parte ecuacional, y coherencia de ecuaciones y reglas).



### 5 - En el módulo ABSTRACT-BAKERY, ¿es finito el espacio de búsqueda alcanzable a partir de estados definidos con el operador initial?



### 6 - Utiliza el comprobador de modelos de Maude para comprobar la exclusión mutua del sistema con 5 procesos.



### 7 - Utiliza el comprobador de modelos de Maude para comprobar si hay estados de bloqueo.



## Ejercicio 2: La panadería modificada

### 8 - Analiza la confluencia, terminación y coherencia del sistema definido.



### 9 - ¿Es finito el espacio de búsqueda alcanzable a partir de estados definidos con el operador initial? Utiliza el comando search para comprobar la exclusión mutua del sistema con 5 procesos.



### 10 - La abstracción proporcionada por el módulo ABSTRACT-BAKERY no es suficiente para este sistema modificado, ¿por qué? Especifica una abstracción válida para este nuevo sistema en una módulo ABSTRACT-BAKERY+.



### 11 - Utiliza la abstracción anterior para comprobar la no existencia de bloqueos y la exclusión mutua



## Ejercicio 3: El lenguaje PARALLEL++

### 12 - Comprueba utilizando el comando search la ausencia de bloqueo y la exclusión mutua de esa versión del algoritmo