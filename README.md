rnch / nrnch
============

Nuestro bien ponderado amigo [Renich](https://github.com/renich) es conocido
por nombrar hosts de manera abreviada por medio de la eliminación de vocales
del concepto que nombra al host, lo que ahorra tiempo de tecleo en cada
invocación a SSH.

Para simplificar esta tarea y bromear a costa de él, se presentan a
continuación dos scripts, `rnch` y `nrnch`, que renichea y desrenichea,
respectivamente, la palabra que se pase por entrada estándar.

Como benefio colateral, se propone que también puedan usarse para ahorrar
ancho de banda y latencia en transmisiones basadas en el
[RFC 1149](https://es.wikipedia.org/wiki/IP_sobre_palomas_mensajeras) al
reducir la longitud y peso de los paquetes IP. Se requiere de mayor
investigación en esta área.

Para facilitar el uso de estas herramientas se ofrecen las ligas simbólicas:
`renich -> rnch` y `unrenich -> nrnch`.


`renich -> rnch`
----------------

Este script recibe una palabra por entrada estándar y la renichea por medio
de algoritmos de AI (porque #2024).

Ejemplo de invocación:

```
$ echo dictionary | ./renich
dctnry
```


`unrenich -> nrnch`
-------------------

Este script aplica el procedimiento inverso: recibe una palabra
renicheada por entrada estándar y la desrenichea, mostrando las posibles
palabras origen. Se puede especificar el idioma de origen por medio del
primer argumento, cuyo archivo de diccionario debe existir en
`/usr/share/dict`. En caso de omitirse, el idioma por defecto se
considera `words` que típicamente correspondiente a inglés. Debido a la
complejidad computacional, no es posible utilizar AI en este script.

Ejemplo de invocación:

```
$ echo dctnry | ./unrenich
server

$ echo srvdr | ./unrenich spanish
servador
servidera
servidero
servidor
servidora
```


Estilo de código
----------------

Los nombres de las variables deben estar renicheadas, según lo ejemplifica
el código de `nrnch`:

```
#!/bin/sh

DCTNRYFL=/usr/share/dict/words
[ -n "$1" ] && DCTNRYFL="/usr/share/dict/$1"

RGLRXPRSSN="$(sed -re 's/(.)/[aeiou]*\1[aeiou]*/g')"
egrep "^$RGLRXPRSSN$" "$DCTNRYFL"
```
