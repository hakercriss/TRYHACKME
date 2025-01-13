# Argumentos, Variables y Arrays

## Argumentos
La ventaja de los scripts bash es que siempre podemos pasar hasta 9 argumentos ($0-$9) al script sin asignarlos a variables ni establecer los correspondientes requisitos para éstas. 9 argumentos porque el primer argumento '$0' está reservado para el script. Como podemos ver aquí, necesitamos el signo de dólar ($) antes del nombre de la variable para usarla en la posición especificada. La asignación se vería así en comparación:
```console
TheNob@htb[/htb]$ ./script.sh ARG1 ARG2 ARG3 ... ARG9
       ASSIGNMENTS:       $0      $1   $2   $3 ...   $9
```
Esto significa que hemos asignado automáticamente los argumentos correspondientes a las variables predefinidas en este lugar. Estas variables se denominan variables especiales. Estas variables especiales sirven como marcadores de posición. Si ahora volvemos a mirar la sección de código, veremos dónde y qué argumentos se han utilizado.

### CIDR.sh
```console
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

<SNIP>
```

Hay varias formas de ejecutar nuestro script. Sin embargo, primero debemos establecer los privilegios de ejecución del script antes de ejecutarlo con el intérprete definido en él.

### CIDR.sh - Establecer privilegios de ejecución
```console
TheNob@htb[/htb]$ chmod +x cidr.sh
```
### CIDR.sh - Ejecución sin Argumentos
```console
TheNob@htb[/htb]$ ./cidr.sh

You need to specify the target domain.

Usage:
	cidr.sh <domain>
```
### CIDR.sh - Ejecución sin Permisos de Ejecución
```console
TheNob@htb[/htb]$ bash cidr.sh

You need to specify the target domain.

Usage:
	cidr.sh <domain>
```

## Variables especiales
Las variables especiales utilizan el Separador Interno de Campos (IFS) para identificar cuando termina un argumento y comienza el siguiente. Bash proporciona varias variables especiales que ayudan durante la ejecución de scripts. Algunas de estas variables son:

|IFS|Descripción|
|-|-|
|$#|Esta variable contiene el número de argumentos pasados al script.|
|$@|Esta variable se puede utilizar para recuperar la lista de argumentos de la línea de comandos.|
|$n|Cada argumento de la línea de comandos se puede recuperar selectivamente utilizando su posición. Por ejemplo, el primer argumento se encuentra en $1.|
|$$| El ID del proceso que se está ejecutando actualmente.|
|$?|	El estado de salida del script. Esta variable es útil para determinar el éxito de un comando. El valor 0 representa una ejecución exitosa, mientras que 1 es el resultado de un fallo.|

De las mostradas arriba, tenemos 3 de estas variables especiales en nuestra condición if-else.

|IFS|Descripción|
|-|-|
|$#|En este caso, sólo necesitamos una variable que debe ser asignada a la variable de dominio. Esta variable se utiliza para especificar el objetivo con el que queremos trabajar. Si proporcionamos sólo un FQDN como argumento, la variable $# tendrá el valor 1.|
|$0|A esta variable especial se le asigna el nombre del script ejecutado.|
|$1|Separado por un espacio, el primer argumento se asigna a esa variable especial.|

## Variables
También vemos al final del bucle if-else que asignamos el valor del primer argumento a la variable llamada «dominio». La asignación de variables se realiza sin el signo del dólar ($). El signo del dólar sólo sirve para que el valor correspondiente a esta variable pueda ser utilizado en otras secciones de código. Al asignar variables, no debe haber espacios entre los nombres y los valores.
```console
<SNIP>
else
	domain=$1
fi
<SNIP>
```

A diferencia de otros lenguajes de programación, en Bash no existe una diferenciación y reconocimiento directo entre los tipos de variables como «cadenas», «enteros» y «booleanos». Todos los contenidos de las variables se tratan como caracteres de cadena. Bash habilita funciones aritméticas dependiendo de si sólo se asignan números o no. Es importante tener en cuenta al declarar variables que éstas no contengan un espacio. De lo contrario, el nombre real de la variable se interpretará como una función interna o un comando.

Declarar una variable - Error
```console
TheNob@htb[/htb]$ variable = "this will result with an error."

command not found: variable
```
Declarar una variable - Sin error
```console
TheNob@htb[/htb]$ variable="Declared without an error."
TheNob@htb[/htb]$ echo $variable

Declared without an error.
```

## Arrays
También existe la posibilidad de asignar varios valores a una única variable en Bash. Esto puede ser beneficioso si queremos escanear múltiples dominios o direcciones IP. Estas variables se denominan arrays que podemos utilizar para almacenar y procesar una secuencia ordenada de valores de tipo específico. Los arrays identifican cada entrada almacenada con un índice que empieza por 0. Cuando queremos asignar un valor a un componente de un array, lo hacemos de la misma forma que con las variables estándar del shell. Todo lo que hacemos es especificar el índice del campo encerrado entre corchetes. La declaración para arrays tiene este aspecto en Bash:

### Arrays.sh
```console
#!/bin/bash

domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)

echo ${domains[0]}
```
También podemos recuperarlos individualmente utilizando el índice mediante la variable con el índice correspondiente entre llaves. Las llaves se utilizan para la expansión de variables.
```console
TheNob@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com
```
Es importante tener en cuenta que las comillas simples (' ... ') y las comillas dobles (» ... ») impiden la separación por un espacio de los valores individuales del arrays. Esto significa que todos los espacios entre las comillas simples y dobles se ignoran y se tratan como un único valor asignado al arrays.

### Arrays.sh
```console
#!/bin/bash

domains=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
echo ${domains[0]}
```
```console
TheNob@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com
```
