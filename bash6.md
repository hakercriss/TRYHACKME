# Control de flujo - Bucles

El control del flujo de nuestros scripts es esencial. Ya hemos aprendido sobre las condiciones if-else, que también forman parte del control de flujo. Después de todo, queremos que nuestro script funcione rápida y eficientemente, y para esto, podemos usar otros componentes para incrementar la eficiencia y permitir un procesamiento libre de errores. Cada estructura de control es una rama o un bucle. Las expresiones lógicas de valores booleanos suelen controlar la ejecución de una estructura de control. Estas estructuras de control incluyen:

- Bifurcaciones:
  - Condiciones If-Else
  - Sentencias Case

- Bucles:
  - Bucles For
  - Bucles While
  - Bucles Until

## Bucles For

Comencemos con los bucles For. El bucle For se ejecuta en cada pasada precisamente para un parámetro, que el shell toma de una lista, calcula a partir de un incremento o toma de otra fuente de datos. El bucle For se ejecuta mientras encuentre los datos correspondientes. Este tipo de bucle puede estructurarse y definirse de diferentes maneras. Por ejemplo, los bucles for se utilizan a menudo cuando necesitamos trabajar con muchos valores diferentes de un arrays. Se puede utilizar para escanear diferentes hosts o puertos. También podemos usarlo para ejecutar comandos específicos para puertos conocidos y sus servicios para acelerar nuestro proceso de enumeración. La sintaxis para esto puede ser la siguiente:

### Sintaxis - Ejemplos
```console
for variable in 1 2 3 4
do
	echo $variable
done
```
```console
for variable in file1 file2 file3
do
	echo $variable
done
```
```console
for ip in "10.10.10.170 10.10.10.174 10.10.10.175"
do
	ping -c 1 $ip
done
```
Por supuesto, también podemos escribir estos comandos en una sola línea. Un comando de este tipo tendría el siguiente aspecto:
```console
TheNob@htb[/htb]$ for ip in 10.10.10.170 10.10.10.174;do ping -c 1 $ip;done

PING 10.10.10.170 (10.10.10.170): 56 data bytes
64 bytes from 10.10.10.170: icmp_seq=0 ttl=63 time=42.106 ms

--- 10.10.10.170 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 42.106/42.106/42.106/0.000 ms
PING 10.10.10.174 (10.10.10.174): 56 data bytes
64 bytes from 10.10.10.174: icmp_seq=0 ttl=63 time=45.700 ms

--- 10.10.10.174 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 45.700/45.700/45.700/0.000 ms
```
Echemos otro vistazo a nuestro script CIDR.sh. Hemos añadido varios bucles for al script, pero quedémonos con esta pequeña sección de código.

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
Como en el ejemplo anterior, para cada dirección IP del arrays «ipaddr» hacemos una petición «whois», cuya salida se filtra por «NetRange» y «CIDR». Esto nos ayuda a determinar en qué rango de direcciones se encuentra nuestro objetivo. Podemos utilizar esta información para buscar hosts adicionales durante una prueba de penetración, si el cliente lo aprueba. Los resultados que recibimos se muestran como corresponde y se almacenan en el archivo «CIDR.txt».

## Bucles while
El bucle while es conceptualmente simple y sigue el siguiente principio:

> - Una sentencia se ejecuta mientras se cumpla una condición (true).

También podemos combinar bucles y unir su ejecución con diferentes valores. Es importante tener en cuenta que la combinación excesiva de varios bucles entre sí puede hacer que el código sea muy poco claro y dar lugar a errores difíciles de encontrar y seguir. Tal combinación puede verse como en nuestro script CIDR.sh.

### CIDR.sh
```console
<SNIP>
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
<SNIP>
```
 Los bucles while también funcionan con condiciones como if-else. Un bucle while necesita algún tipo de contador para orientarse cuando tiene que dejar de ejecutar los comandos que contiene. De lo contrario, esto conduce a un bucle sin fin. Dicho contador puede ser una variable que hayamos declarado con un valor específico o un valor booleano. Los bucles while se ejecutan mientras el valor booleano es «True». Además del contador, también podemos utilizar el comando «break», que interrumpe el bucle al llegar a este comando como en el siguiente ejemplo:

### WhileBreaker.sh
```console
#!/bin/bash

counter=0

while [ $counter -lt 10 ]
do
  # Increase $counter by 1
  ((counter++))
  echo "Counter: $counter"

  if [ $counter == 2 ]
  then
    continue
  elif [ $counter == 4 ]
  then
    break
  fi
done
```
### WhileBreaker.sh
```console
TheNob@htb[/htb]$ ./WhileBreaker.sh

Counter: 1
Counter: 2
Counter: 3
Counter: 4
```
## Bucles Until
También existe el bucle until, que es relativamente raro. Sin embargo, el bucle until funciona exactamente igual que el bucle while, pero con la diferencia:

> - El código dentro de un bucle until se ejecuta mientras la condición particular sea falsa.

La otra forma es dejar que el bucle se ejecute hasta que se alcance el valor deseado. Los bucles «until» son muy adecuados para esto. Este tipo de bucle funciona de forma similar al bucle «while» pero, como ya se ha mencionado, con la diferencia de que se ejecuta hasta que el valor booleano es «False».

### Until.sh
```console
#!/bin/bash

counter=0

until [ $counter -eq 10 ]
do
  # Increase $counter by 1
  ((counter++))
  echo "Counter: $counter"
done
```
### Until.sh
```console
TheNob@htb[/htb]$ ./Until.sh

Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
Counter: 6
Counter: 7
Counter: 8
Counter: 9
Counter: 10
```
## Script de Ejercicio
```console
#!/bin/bash

# Decrypt function
function decrypt {
	MzSaas7k=$(echo $hash | sed 's/988sn1/83unasa/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/4d298d/9999/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/3i8dqos82/873h4d/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/4n9Ls/20X/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/912oijs01/i7gg/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/k32jx0aa/n391s/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/nI72n/YzF1/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/82ns71n/2d49/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/JGcms1a/zIm12/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/MS9/4SIs/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/Ymxj00Ims/Uso18/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/sSi8Lm/Mit/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/9su2n/43n92ka/g')
	Mzns7293sk=$(echo $MzSaas7k | sed 's/ggf3iunds/dn3i8/g')
	MzSaas7k=$(echo $Mzns7293sk | sed 's/uBz/TT0K/g')

	flag=$(echo $MzSaas7k | base64 -d | openssl enc -aes-128-cbc -a -d -salt -pass pass:$salt)
}

# Variables
var="9M"
salt=""
hash="VTJGc2RHVmtYMTl2ZnYyNTdUeERVRnBtQWVGNmFWWVUySG1wTXNmRi9rQT0K"

# Base64 Encoding Example:
#        $ echo "Some Text" | base64

# <- For-Loop here

# Check if $salt is empty
if [[ ! -z "$salt" ]]
then
	decrypt
	echo $flag
else
	exit 1
fi
```


