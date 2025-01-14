# Entrada y salida

## Control de Entrada
Podemos obtener resultados de nuestras peticiones enviadas y comandos ejecutados, sobre los que tenemos que decidir manualmente cómo proceder. Otro ejemplo sería que hayamos definido varias funciones en nuestro script diseñadas para diferentes escenarios. Tenemos que decidir cuál de ellas debe ejecutarse tras una comprobación manual y en función de los resultados. También es muy posible que no se permita la ejecución de determinados escaneos o actividades. Por lo tanto, necesitamos estar familiarizados con cómo hacer que un script en ejecución espere nuestras instrucciones. Si volvemos a mirar nuestro script CIDR.sh, veremos que hemos añadido una llamada de este tipo para decidir los pasos a seguir.

### CIDR.sh
```console
# Available options
<SNIP>
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

Las primeras líneas de eco sirven como menú de visualización de las opciones que tenemos disponibles. Con el comando read, se muestra la línea con «Select your option:», y la opción adicional -p asegura que nuestra entrada permanezca en la misma línea. Nuestra entrada se almacena en la variable opt, que luego utilizamos para ejecutar las funciones correspondientes con la sentencia case, que veremos más adelante. Dependiendo del número que introduzcamos, la sentencia case determina qué funciones se ejecutan.

## Control de salida
Ya hemos aprendido sobre las redirecciones de salida en el módulo Fundamentos de Linux. Sin embargo, el problema con las redirecciones es que no obtenemos ninguna salida del comando respectivo. Será redirigida al archivo apropiado. Si nuestros scripts se complican más tarde, pueden tomar mucho más tiempo que unos pocos segundos. Para evitar sentarnos inactivamente y esperar los resultados de nuestro script, podemos usar la utilidad tee. Nos asegura que vemos los resultados que obtenemos inmediatamente y que se almacenan en los archivos correspondientes. En nuestro script CIDR.sh, hemos utilizado esta utilidad dos veces de diferentes maneras.

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

# Identify IP address of the specified domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)

<SNIP>
```
Al utilizar tee, transferimos la salida recibida y utilizamos la tubería (|) para reenviarla a tee. El parámetro «-a / --append» garantiza que el archivo especificado no se sobrescriba, sino que se complemente con los nuevos resultados. Al mismo tiempo, nos muestra los resultados y cómo se encontrarán en el fichero.
```console
TheNob@htb[/htb]$ cat discovered_hosts.txt CIDR.txt

165.22.119.202
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16
```
