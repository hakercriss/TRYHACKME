# Aritmética
En Bash, tenemos siete operadores aritméticos diferentes con los que podemos trabajar. Estos se utilizan para realizar diferentes operaciones matemáticas o para modificar ciertos enteros.

## Operadores Aritméticos
|Operador|Descripción|
|-|-|
|+ |Suma|
|- |Sustracción|
|* |Multiplicación|
|/ |División|
| %| Módulo|
|variable++| Aumenta el valor de la variable en 1|
|variable--| Disminuye el valor de la variable en 1|

Podemos resumir todos estos operadores en un pequeño script:

### Arithmetic.sh
```console
#!/bin/bash

increase=1
decrease=1

echo "Addition: 10 + 10 = $((10 + 10))"
echo "Subtraction: 10 - 10 = $((10 - 10))"
echo "Multiplication: 10 * 10 = $((10 * 10))"
echo "Division: 10 / 10 = $((10 / 10))"
echo "Modulus: 10 % 4 = $((10 % 4))"

((increase++))
echo "Increase Variable: $increase"

((decrease--))
echo "Decrease Variable: $decrease"
```
La salida de este script tiene el siguiente aspecto:

### Arithmetic.sh - Ejecución
```console
TheNob@htb[/htb]$ ./Arithmetic.sh

Addition: 10 + 10 = 20
Subtraction: 10 - 10 = 0
Multiplication: 10 * 10 = 100
Division: 10 / 10 = 1
Modulus: 10 % 4 = 2
Increase Variable: 2
Decrease Variable: 0
```

También podemos calcular la longitud de la variable. Usando esta función ${#variable}, cada caracter es contado, y obtenemos el número total de caracteres en la variable.

### VarLength.sh
```console
#!/bin/bash

htb="HackTheBox"

echo ${#htb}
```

### VarLength.sh
```console
TheNob@htb[/htb]$ ./VarLength.sh

10
```
Si observamos nuestro script CIDR.sh, veremos que hemos utilizado varias veces los operadores de incremento y decremento. Esto asegura que el bucle while, del que hablaremos más adelante, se ejecuta y hace ping a los hosts mientras la variable «stat» tiene un valor de 1. Si el comando ping termina con el código 0 (éxito), obtenemos un mensaje de que el host está levantado y la variable «stat», así como las variables «hosts_up» y «hosts_total» se modifican.

### CIDR.sh
```console
<SNIP>
	echo -e "\nPinging host(s):"
	for host in $cidr_ips
	do
		stat=1
		while [ $stat -eq 1 ]
		do
			ping -c 2 $host > /dev/null 2>&1
			if [ $? -eq 0 ]
			then
				echo "$host is up."
				((stat--))
				((hosts_up++))
				((hosts_total++))
			else
				echo "$host is down."
				((stat--))
				((hosts_total++))
			fi
		done
	done
<SNIP>
```
