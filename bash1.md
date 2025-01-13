# Ejecución condicional

La ejecución condicional nos permite controlar el flujo de nuestro script alcanzando diferentes condiciones. Esta función es uno de los componentes esenciales. De lo contrario, sólo podríamos ejecutar un comando tras otro.

Al definir varias condiciones, especificamos qué funciones o secciones de código deben ejecutarse para un valor específico. Si alcanzamos una condición específica, sólo se ejecuta el código para esa condición, y se saltan las demás. Tan pronto como se complete la sección de código, los siguientes comandos se ejecutarán fuera de la ejecución condicional. Veamos de nuevo la primera parte del script y analicémosla.

### Script.sh
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

En resumen, esta sección de código funciona con los siguientes componentes:

- #!/bin/bash - Shebang.
- if-else-fi - Ejecución condicional.
- echo - Imprime una salida específica.
- $# / $0 / $1 - Variables especiales.
- domain - Variables.

Las condiciones de las ejecuciones condicionales pueden definirse utilizando variables ($#, $0, $1, dominio), valores (0) y cadenas, como veremos en los próximos ejemplos. Estos valores se comparan con los operadores de comparación (-eq) que veremos en la siguiente sección.

### Shebang
La línea shebang está siempre en la parte superior de cada script y siempre comienza con «#!». Esta línea contiene la ruta al intérprete especificado (/bin/bash) con el que se ejecuta el script. También podemos usar Shebang para definir otros intérpretes como Python, Perl y otros.
```console
#!/usr/bin/env python
```
```console
#!/usr/bin/env perl
```

### If-Else-Fi
Una de las tareas más fundamentales de la programación es la comprobación de diferentes condiciones. La comprobación de condiciones suele tener dos formas diferentes en los lenguajes de programación y scripting, la condición if-else y las sentencias case. En pseudocódigo, la condición if significa lo siguiente:

### Pseudocódigo
```console
if [ the number of given arguments equals 0 ]
then
	Print: "You need to specify the target domain."
	Print: "<empty line>"
	Print: "Usage:"
	Print: "   <name of the script> <domain>"
	Exit the script with an error
else
	The "domain" variable serves as the alias for the given argument 
finish the if-condition
```
Por defecto, una condición If-Else sólo puede contener un único «If», como se muestra en el siguiente ejemplo.

### If-Only.sh
```console
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
        echo "Given argument is greater than 10."
fi
```
### If-Only.sh - Ejecución
```console
TheNob@htb[/htb]$ bash if-only.sh 5
```
```console
TheNob@htb[/htb]$ bash if-only.sh 12

Given argument is greater than 10.
```
Al añadir Elif o Else, añadimos alternativas para tratar valores o estados específicos. Si un valor particular no se aplica al primer caso, será capturado por los otros.

### If-Elif-Else.sh
```bash
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
	echo "Given argument is greater than 10."
elif [ $value -lt "10" ]
then
	echo "Given argument is less than 10."
else
	echo "Given argument is not a number."
fi
```
### If-Elif-Else.sh - Ejecución
```console
TheNob@htb[/htb]$ bash if-elif-else.sh 5

Given argument is less than 10.
```
```console
TheNob@htb[/htb]$ bash if-elif-else.sh 12

Given argument is greater than 10.
```
```console
TheNob@htb[/htb]$ bash if-elif-else.sh HTB

if-elif-else.sh: line 5: [: HTB: integer expression expected
if-elif-else.sh: line 8: [: HTB: integer expression expected
Given argument is not a number.
```
Podríamos ampliar nuestro script y especificar varias condiciones. Esto podría ser algo como esto

### Varias Condiciones - Script.sh
```console
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
elif [ $# -eq 1 ]
then
	domain=$1
else
	echo -e "Too many arguments given."
	exit 1
fi

<SNIP>
```
Aquí definimos otra condición (elif [<condición>];then) que imprime una línea diciéndonos (echo -e «...») que hemos dado más de un argumento y sale del programa con un error (salida 1).

### Ejercicio Script
```console
#!/bin/bash
# Count number of characters in a variable:
#     echo $variable | wc -c

# Variable to encode
var="nef892na9s1p9asn2aJs71nIsm"

for counter in {1..40}
do
        var=$(echo $var | base64)
done
```
