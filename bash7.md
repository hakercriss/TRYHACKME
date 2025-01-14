# Control de flujo - Ramas

Como ya hemos visto, las ramas en el control de flujo incluyen las sentencias if-else y case. Ya hemos discutido las sentencias if-else en detalle y sabemos cómo funcionan. Ahora veremos más de cerca las sentencias case.

## Sentencias Case
Las sentencias case también se conocen como sentencias switch-case en otros lenguajes, como C/C++ y C#. La principal diferencia entre if-else y switch-case es que las construcciones if-else nos permiten comprobar cualquier expresión booleana, mientras que switch-case siempre compara sólo la variable con el valor exacto. Por lo tanto, las mismas condiciones que para if-else, como «mayor que», no están permitidas para switch-case. La sintaxis de las sentencias switch-case es la siguiente:

### Sintaxis - Switch-Case
```console
case <expression> in
	pattern_1 ) statements ;;
	pattern_2 ) statements ;;
	pattern_3 ) statements ;;
esac
```
La definición de switch-case comienza con case, seguido de la variable o valor como expresión, que se compara en el patrón. Si la variable o valor coincide con la expresión, entonces las sentencias se ejecutan después del paréntesis y terminan con un doble punto y coma (;;).

En nuestro script CIDR.sh, hemos utilizado una sentencia case de este tipo. Aquí definimos cuatro opciones diferentes que asignamos a nuestro script, cómo debe proceder después de nuestra decisión.

### CIDR.sh
```console
<SNIP>
# Available options
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
<SNIP>
```

Con las dos primeras opciones, este script ejecuta diferentes funciones que habíamos definido antes. Con la tercera opción, ambas funciones son ejecutadas, y con cualquier otra opción, el script será terminado.
