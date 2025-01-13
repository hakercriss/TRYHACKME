# Bourne Again Shell

Bash es el lenguaje de scripting que utilizamos para comunicarnos con los SO basados en Unix y dar comandos al sistema. Desde mayo de 2019, Windows proporciona un Subsistema Windows para Linux que nos permite utilizar Bash en un entorno Windows. Es imprescindible dominar el lenguaje para trabajar eficientemente con él. La principal diferencia entre los lenguajes de scripting y programación es que no necesitamos compilar el código para ejecutar el lenguaje de scripting, a diferencia de los lenguajes de programación.

Como probadores de penetración, debemos ser capaces de trabajar con cualquier sistema operativo, ya sea Windows o Unix. La eficacia depende principalmente del conocimiento de los sistemas, especialmente en el campo de la escalada de privilegios. En los sistemas basados en Unix, es esencial aprender a utilizar el terminal, filtrar datos y automatizar estos procesos. Especialmente en grandes redes empresariales basadas en Unix, tendremos que tratar con grandes cantidades de datos. Tenemos que clasificar y filtrar en consecuencia para determinar posibles lagunas e información lo más rápidamente posible.

También es esencial aprender a combinar varios comandos y trabajar con resultados individuales. Aquí es donde entran en juego los scripts, que aumentan nuestra velocidad y eficacia. Al igual que un lenguaje de programación, un lenguaje de scripting tiene casi la misma estructura, que se puede dividir en:

- Entrada y Salida
- Argumentos, variables y matrices
- Ejecución condicional
- Aritmética
- Bucles
- Operadores de comparación
- Funciones

A menudo es común automatizar algunos procesos para no repetirlos todo el tiempo o procesar y filtrar una gran cantidad de información. En general, un script no crea un proceso, sino que es ejecutado por el intérprete que ejecuta el script, en este caso, el Bash. Para ejecutar un script, tenemos que especificar el intérprete y decirle qué script debe procesar. Una llamada de este tipo tiene el siguiente aspecto


Ejecución de scripts - Ejemplos

```console
TheNob@htb[/htb]$ bash script.sh <optional arguments>
```
```console
TheNob@htb[/htb]$ sh script.sh <optional arguments>
```
```console
TheNob@htb[/htb]$ ./script.sh <optional arguments>
```
Veamos un script de este tipo y veamos cómo se pueden crear para obtener resultados específicos. Si ejecutamos este script y especificamos un dominio, veremos qué información nos proporciona este script.

CIDR.sh
```console
TheNob@htb[/htb]$ ./CIDR.sh inlanefreight.com

Discovered IP address(es):
165.22.119.202

Additional options available:
	1) Identify the corresponding network range of target domain.
	2) Ping discovered hosts.
	3) All checks.
	*) Exit.

Select your option: 3

NetRange for 165.22.119.202:
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16

Pinging host(s):
165.22.119.202 is up.

1 out of 1 hosts are up.
```

Ahora veamos ese script en detalle y leamos línea por línea de la mejor manera posible. En las próximas secciones, veremos y analizaremos todas las partes de este script.

CIDR.sh
```bash
#!/bin/bash

# Comprobación de los argumentos dados
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

# Identificar el rango de red para la(s) dirección(es) IP especificada(s)
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

# Dirección(es) IP descubierta(s)
function ping_host {
	hosts_up=0
	hosts_total=0
	
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
	
	echo -e "\n$hosts_up out of $hosts_total hosts are up."
}

# Identificar la dirección IP del dominio especificado
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)

echo -e "Discovered IP address:\n$hosts\n"
ipaddr=$(host $domain | grep "has address" | cut -d" " -f4 | tr "\n" " ")

# Opciones disponibles
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```

Como podemos ver, hemos comentado aquí varias partes del script en las que podemos dividirlo.

- Comprobar los argumentos dados
- Identificar el rango de red para la(s) dirección(es) IP especificada(s)
- Hacer ping a la(s) dirección(es) IP descubierta(s)
- Identificar dirección(es) IP del dominio especificado
- Opciones disponibles

### 1. Comprobar los argumentos dados
En la primera parte del script, tenemos una sentencia if-else que comprueba si hemos especificado un dominio que represente a la empresa objetivo.

### 2. Identificar el rango de red para la(s) dirección(es) IP especificada(s)
Aquí hemos creado una función que hace una consulta «whois» para cada dirección IP y muestra la línea para el rango de red reservado, y lo almacena en el CIDR.txt.

### 3. Ping dirección(es) IP descubierta(s)
Esta función adicional se utiliza para comprobar si los hosts encontrados son alcanzables con las respectivas direcciones IP. Con el bucle For, hacemos ping a cada dirección IP del rango de red y contamos los resultados.

### 4. Identificar la(s) dirección(es) IP del dominio especificado
Como primer paso en este script, identificamos la dirección IPv4 del dominio que se nos devuelve.

### 5. Opciones disponibles
A continuación, decidimos qué funciones queremos utilizar para obtener más información sobre la infraestructura.
