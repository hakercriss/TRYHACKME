Operadores de comparación
Para comparar valores específicos entre sí, necesitamos elementos que se denominan operadores de comparación. Los operadores de comparación se utilizan para determinar cómo se compararán los valores definidos. Para estos operadores, diferenciamos entre:

operadores de cadena
operadores de enteros
operadores de fichero
operadores booleanos
Operadores de cadena
Si comparamos cadenas, entonces sabemos lo que nos gustaría tener en el valor correspondiente.

Descripción del operador
== es igual a
!= no es igual a
< es menor que en orden alfabético ASCII
> es mayor que en orden alfabético ASCII
-z si la cadena está vacía (null)
-n si la cadena no es nula

Es importante notar aquí que ponemos la variable para el argumento dado ($1) entre comillas dobles («$1»). Esto indica a Bash que el contenido de la variable debe tratarse como una cadena. De lo contrario, obtendríamos un error.

Los operadores de comparación de cadenas «< / >» sólo funcionan dentro de los dobles corchetes [[ <condición> ]]. Podemos encontrar la tabla ASCII en Internet o utilizando el siguiente comando en el terminal. Más adelante veremos un ejemplo.

ASCII significa American Standard Code for Information Interchange y representa una codificación de caracteres de 7 bits. Dado que cada bit puede tomar dos valores, existen 128 patrones de bits diferentes, que también pueden interpretarse como los enteros decimales 0 - 127 o en valores hexadecimales 00 - 7F. Los 32 primeros códigos de caracteres ASCII se reservan como caracteres de control.

Operadores de números enteros
La comparación de números enteros puede resultarnos muy útil si sabemos qué valores queremos comparar. En consecuencia, definimos los siguientes pasos y comandos de cómo el script debe tratar el valor correspondiente.

Descripción del Operador
-eq es igual a
-ne no es igual a
-lt es menor que
-le es menor o igual que
-gt es mayor que
-ge es mayor o igual que

Operadores de archivo
Los operadores de fichero son útiles si queremos averiguar permisos concretos o si existen.

Operador Descripción
-e si el fichero existe
-f comprueba si es un fichero
-d comprueba si es un directorio
-L comprueba si es un enlace simbólico
-N comprueba si el fichero ha sido modificado después de su última lectura
-O si el usuario actual es el propietario del archivo
-G si el identificador de grupo del archivo coincide con el del usuario actual
-s comprueba si el archivo tiene un tamaño superior a 0
-r comprueba si el archivo tiene permiso de lectura
-w comprueba si el archivo tiene permiso de escritura
-x comprueba si el archivo tiene permiso de ejecución

Operadores booleanos y lógicos
Con los operadores lógicos obtenemos como resultado un valor booleano «falso» o «verdadero». Bash nos da la posibilidad de comparar cadenas utilizando dobles corchetes [[ <condición> ]]. Para obtener estos valores booleanos, podemos utilizar los operadores de cadena. Tanto si la comparación coincide como si no, obtenemos el valor booleano «false» o «true».


Operadores lógicos
Con los operadores lógicos, podemos definir varias condiciones dentro de una. Esto significa que todas las condiciones que definamos deben coincidir antes de que se pueda ejecutar el código correspondiente.

Descripción del operador
! negociación lógica NOT
&& AND lógico
|| OR lógico


Ejercicio Script




