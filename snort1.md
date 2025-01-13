# Introducción a IDS/IPS

Antes de sumergirnos en Snort y en el análisis del tráfico, hagamos un breve repaso de lo que es un Sistema de Detección de Intrusiones (IDS) y un Sistema de Prevención de Intrusiones (IPS). Es posible configurar tu infraestructura de red y utilizar ambos, pero antes de empezar a utilizar cualquiera de ellos, aprendamos las diferencias.

Sistema de detección de intrusiones (IDS)

El IDS es una solución de monitorización pasiva para detectar posibles actividades/patrones maliciosos, incidentes anómalos y violaciones de políticas. Se encarga de generar alertas para cada evento sospechoso. 

Existen dos tipos principales de sistemas IDS;

Network Intrusion Detection System (NIDS) - NIDS monitoriza el flujo de tráfico de varias áreas de la red. El objetivo es investigar el tráfico en toda la subred. Si se identifica una firma, se crea una alerta.

Sistema de detección de intrusiones basado en host (HIDS) - El HIDS monitoriza el flujo de tráfico desde un único dispositivo. El objetivo es investigar el tráfico en un dispositivo concreto. Si se identifica una firma, se crea una alerta.

Sistema de prevención de intrusiones (IPS)
IPS es una solución de protección activa para prevenir posibles actividades/patrones maliciosos, incidentes anómalos y violaciones de políticas. Se encarga de detener/prevenir/terminar el evento sospechoso tan pronto como se realiza la detección.

 Existen cuatro tipos principales de sistemas IPS;

- Network Intrusion Prevention System (NIPS) - NIPS monitoriza el flujo de tráfico de varias áreas de la red. El objetivo es proteger el tráfico en toda la subred. Si se identifica una firma, se interrumpe la conexión.

- Sistema de prevención de intrusiones basado en el comportamiento (Network Behaviour Analysis - NBA) - Los sistemas basados en el comportamiento monitorizan el flujo de tráfico desde varias áreas de la red. El objetivo es proteger el tráfico en toda la subred. Si se identifica una firma, se interrumpe la conexión.

El sistema de análisis del comportamiento de la red funciona de forma similar al NIPS. La diferencia entre el NIPS y el basado en el comportamiento es que los sistemas basados en el comportamiento requieren un periodo de entrenamiento (también conocido como «baselining») para aprender el tráfico normal y diferenciar el tráfico malicioso y las amenazas. Este modelo proporciona resultados más eficaces contra las nuevas amenazas.

El sistema se entrena para conocer lo «normal» para detectar lo «anormal». El periodo de entrenamiento es crucial para evitar falsos positivos. En caso de que se produzca algún fallo de seguridad durante el periodo de entrenamiento, los resultados serán muy problemáticos. Otro punto crítico es asegurarse de que el sistema está bien entrenado para reconocer actividades benignas. 

- Sistema de prevención de intrusiones inalámbricas (WIPS) - WIPS monitoriza el flujo de tráfico de la red inalámbrica. El objetivo es proteger el tráfico inalámbrico y detener posibles ataques lanzados desde allí. Si se identifica una firma, se interrumpe la conexión.

- Sistema de prevención de intrusiones basado en host (HIPS) - HIPS protege activamente el flujo de tráfico desde un único dispositivo terminal. El objetivo es investigar el tráfico en un dispositivo concreto. Si se identifica una firma, se interrumpe la conexión.

El mecanismo de funcionamiento de HIPS es similar al de HIDS. La diferencia entre ellos es que mientras HIDS crea alertas de amenazas, HIPS detiene las amenazas terminando la conexión.


## Técnicas de detección/prevención

Existen tres técnicas principales de detección y prevención utilizadas en las soluciones IDS e IPS;

#### Basado en firmas
Esta técnica se basa en reglas que identifican los patrones específicos del comportamiento malicioso conocido.Este modelo ayuda a detectar amenazas conocidas. 

#### Basada en el comportamiento
Esta técnica identifica nuevas amenazas con nuevos patrones que traspasan las firmas.El modelo compara los comportamientos conocidos/normales con los desconocidos/anormales.Este modelo ayuda a detectar amenazas previamente desconocidas o nuevas.

#### Basada en políticas 
Esta técnica compara las actividades detectadas con la configuración del sistema y las políticas de seguridad.Este modelo ayuda a detectar violaciones de las políticas.

## Resumen

¡Uf! Ha sido un viaje largo y con mucha información.Resumamos las funciones generales de los IDS y los IPS en pocas palabras.

- Los IDS pueden identificar las amenazas, pero necesitan la ayuda del usuario para detenerlas.

- Los IPS pueden identificar y bloquear las amenazas con menos asistencia del usuario en el momento de la detección.

> Hablemos ahora de Snort.Aquí está el resto de la descripción oficial del snort;«Snort también puede desplegarse en línea para detener estos paquetes.Snort tiene tres usos principales:Como un rastreador de paquetes como tcpdump, como un registrador de paquetes - que es útil para la depuración del tráfico de red, o puede ser utilizado como un sistema de prevención de intrusiones en la red en toda regla. Snort puede descargarse y configurarse tanto para uso personal como empresarial».

SNORT es un sistema de prevención y detección de intrusiones en la red (NIDS/NIPS) de código abierto basado en reglas.Fue desarrollado y sigue siendo mantenido por Martin Roesch, colaboradores de código abierto y el equipo Cisco Talos. 

Capacidades de Snort;

- Análisis de tráfico en tiempo real
- Detección de ataques y sondas
- Registro de paquetes
- Análisis de protocolos
- Alertas en tiempo real
- Módulos y plugins
- Preprocesadores
- Soporte multiplataforma(Linux y Windows)

Snort tiene tres modelos de uso principales;

- Modo Sniffer - Lee paquetes IP y los muestra en la aplicación de consola.
- Modo Packet Logger - Registra todos los paquetes IP (entrantes y salientes) que visitan la red.
- Modos NIDS (Sistema de Detección de Intrusos en la Red) y NIPS (Sistema de Prevención de Intrusos en la Red) - Registra/elimina los paquetes que se consideran maliciosos de acuerdo con las reglas definidas por el usuario.



