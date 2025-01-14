# Funciones
Cuanto más grandes son nuestros scripts, más caóticos se vuelven. Si utilizamos las mismas rutinas varias veces en el script, el tamaño del script aumentará en consecuencia. En estos casos, las funciones son la solución que mejora muchas veces tanto el tamaño como la claridad del script. Combinamos varios comandos en un bloque entre llaves ( { ... } ) y los llamamos con un nombre de función definido por nosotros con funciones. Una vez definida una función, puede ser llamada y utilizada de nuevo durante el script.

Las funciones son una parte esencial de los scripts y programas, ya que se utilizan para ejecutar comandos recurrentes para diferentes valores y fases del script o programa. Por lo tanto, no tenemos que repetir toda la sección de código repetidamente, sino que podemos crear una única función que ejecute los comandos específicos. La definición de este tipo de funciones facilita la lectura del código y ayuda a mantenerlo lo más corto posible. Es importante tener en cuenta que las funciones siempre deben definirse lógicamente antes de la primera llamada, ya que un script también se procesa de arriba a abajo. Por lo tanto la definición de una función está siempre al principio del script. Existen dos métodos para definir las funciones:

### Método 1 - Funciones
```console
function name {
	<commands>
}
```
### Método 2 - Funciones
```console
name() {
	<commands>
}
```
Podemos elegir el método para definir una función que nos resulte más cómodo. En nuestro script CIDR.sh, usamos el primer método porque es más fácil de leer con la palabra clave «función».

### CIDR.sh
```console
<SNIP>
# Identify Network range for the specified IP address(es)
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}
<SNIP>
```
La función se llama únicamente llamando al nombre especificado de la función, como hemos visto en la sentencia case.

### Ejecución de la Función - CIDR.sh
```console
<SNIP>
case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```
## Paso de parámetros
Estas funciones deben diseñarse de forma que puedan utilizarse con una estructura fija de los valores o, al menos, sólo con un formato fijo. Como ya hemos visto en nuestro script CIDR.sh, utilizamos el formato de una dirección IP para la función «network_range». Los parámetros son opcionales, y por lo tanto podemos llamar a la función sin parámetros. En principio, se aplica lo mismo a los parámetros pasados que a los parámetros pasados a un script de shell. Estos son $1 - $9 (${n}), o $variable como ya hemos visto. Cada función tiene su propio conjunto de parámetros. Por lo que no colisionan con los de otras funciones o los parámetros del script de shell.

Una diferencia importante entre los scripts bash y otros lenguajes de programación es que todas las variables definidas se procesan siempre globalmente a menos que se declare lo contrario por «local». Esto significa que la primera vez que hayamos definido una variable en una función, la llamaremos en nuestro script principal (fuera de la función). Pasar los parámetros a las funciones se hace de la misma forma que pasamos los argumentos a nuestro script y tiene el siguiente aspecto:

### PrintPars.sh
```console
#!/bin/bash

function print_pars {
	echo $1 $2 $3
}

one="First parameter"
two="Second parameter"
three="Third parameter"

print_pars "$one" "$two" "$three"
```
```console
TheNob@htb[/htb]$ ./PrintPars.sh

First parameter Second parameter Third parameter
```

## Valores de retorno
Cuando iniciamos un nuevo proceso, cada proceso hijo (por ejemplo, una función en el script ejecutado) devuelve un código de retorno al proceso padre (shell bash a través del cual ejecutamos el script) a su terminación, informándole del estado de la ejecución. Esta información se utiliza para determinar si el proceso se ejecutó correctamente o si se produjeron errores específicos. Basándose en esta información, el proceso padre puede decidir sobre el flujo posterior del programa.

|Código de retorno |Descripción|
|-|-|
|1|Errores generales|
|2|Uso incorrecto de shell builtins|
|126 |El comando invocado no puede ejecutarse|
|127 |Comando no encontrado|
|128 |Argumento inválido para salir|
|128+n| Señal de error fatal "n"|
|130 |Script terminado por Control-C|
|255\*| Estado de salida fuera de rango|

Para recuperar el valor de una función, podemos utilizar varios métodos como return, echo, o una variable. En el siguiente ejemplo, veremos cómo usar «$?» para leer el «código de retorno», cómo pasar los argumentos a la función y cómo asignar el resultado a una variable.

### Return.sh
```console
#!/bin/bash

function given_args {

        if [ $# -lt 1 ]
        then
                echo -e "Number of arguments: $#"
                return 1
        else
                echo -e "Number of arguments: $#"
                return 0
        fi
}

# No arguments given
given_args
echo -e "Function status code: $?\n"

# One argument given
given_args "argument"
echo -e "Function status code: $?\n"

# Pass the results of the funtion into a variable
content=$(given_args "argument")

echo -e "Content of the variable: \n\t$content"
```
### Return.sh - Ejecución
```console
TheNob@htb[/htb]$ ./Return.sh

Number of arguments: 0
Function status code: 1

Number of arguments: 1
Function status code: 0

Content of the variable:
    Number of arguments: 1
```


