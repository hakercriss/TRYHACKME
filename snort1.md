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
