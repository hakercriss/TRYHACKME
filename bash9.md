# Depuración

Bash nos ofrece una excelente oportunidad para encontrar, rastrear y corregir errores en nuestro código. El término depuración puede tener muchos significados diferentes. Sin embargo, la depuración de Bash es el proceso de eliminar errores (bugs) de nuestro código. La depuración se puede realizar de muchas maneras diferentes. Por ejemplo, podemos utilizar nuestro código de depuración para comprobar si hay errores tipográficos, o podemos utilizarlo para el análisis de código para rastrearlos y determinar por qué se producen errores específicos.


Este proceso también se utiliza para encontrar vulnerabilidades en los programas. Por ejemplo, podemos intentar provocar errores utilizando diferentes tipos de entrada y rastrear su manejo en la CPU a través del ensamblador, lo que puede proporcionar una forma de manipular el manejo de estos errores para insertar nuestro propio código y forzar al sistema a ejecutarlo. Este tema será cubierto y discutido en detalle en otros módulos. Bash nos permite depurar nuestro código utilizando las opciones «-x» (xtrace) y «-v». Ahora veamos un ejemplo con nuestro script CIDR.sh.


### CIDR.sh - Depuración
```console
TheNob@htb[/htb]$ bash -x CIDR.sh

+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
	CIDR.sh <domain>
+ exit 1
```

Aquí Bash nos muestra con precisión qué función o comando se ejecutó con qué valores. Esto se indica con el signo más (+) al principio de la línea. Si queremos ver todo el código de una función en particular, podemos establecer la opción «-v» que muestra la salida con más detalle.

### CIDR.sh - Depuración detallada
```console
TheNob@htb[/htb]$ bash -x -v CIDR.sh

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
+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
	CIDR.sh <domain>
+ exit 1
```
En comparación con la depuración normal, vemos toda la sección de código que se ha procesado hasta el momento y, a continuación, los pasos individuales que se han dado.
