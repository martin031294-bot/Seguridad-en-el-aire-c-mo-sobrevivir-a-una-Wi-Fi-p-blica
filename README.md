Informe de Auditoría de Red Wi-Fi Insegura
1. Introducción
Como parte de las prácticas de análisis de tráfico y concienciación en seguridad ofensiva y defensiva, este informe documenta la auditoría de una conexión realizada sobre una red Wi-Fi pública no cifrada. El objetivo es evidenciar los riesgos inherentes al uso de protocolos de texto plano como HTTP y demostrar la necesidad de implementar capas de cifrado extremo a extremo, como el uso de VPNs.

2. Sitio Analizado
Para realizar este análisis de tráfico sin comprometer sistemas productivos, se utilizó un sitio web diseñado específicamente para este propósito que carece por completo de redirecciones a HTTPS o políticas HSTS:

URL: [http://neverssl.com](http://neverssl.com)

Propósito: Permitir a los dispositivos conectar a internet en redes públicas cautivas donde los redireccionamientos automáticos de HTTPS fallan, exponiendo claramente una petición HTTP estándar.

3. Evidencia Observada (Parte 1 y Respuestas 1-2)
¿Qué protocolo utiliza el sitio?
El sitio utiliza HTTP (Hypertext Transfer Protocol) sobre el puerto 80. Esto significa que no existe cifrado en la capa de transporte. Cualquier dato enviado o recibido viaja en texto plano (plaintext), lo que permite que cualquier nodo intermedio o dispositivo conectado a la misma red física/inalámbrica pueda interceptar la comunicación mediante herramientas de análisis de paquetes (como Wireshark o tcpdump).

Elementos visibles en la solicitud (Network Tab)
Al inspeccionar la solicitud HTTP inicial en las Herramientas de Desarrollador (F12), se observaron los siguientes parámetros expuestos en claro:

URL Solicitada: [http://neverssl.com/](http://neverssl.com/) (Recurso raíz).

Método HTTP: GET (Solicitud de obtención de recursos sin parámetros sensibles en la URI).

Host: neverssl.com (El dominio de destino al cual se direcciona el tráfico).

Headers de la Petición:

User-Agent: Identifica el sistema operativo y navegador (ej. motor Blink, versión de Windows/Linux).

Accept-Encoding: Tipos de compresión aceptados (gzip, deflate, br).

Host: El servidor objetivo.

Protocolo: http/1.1 o http/2 sin encriptación TLS visible en el handshake de la capa de transporte para ese host específico.

4. Riesgos al Navegar mediante HTTP en Redes Wi-Fi Públicas (Respuesta 3)
Las redes Wi-Fi públicas (cafeterías, aeropuertos, plazas) operan bajo topologías compartidas donde todos los dispositivos conectados "escuchan" o comparten el mismo medio inalámbrico. Los riesgos críticos incluyen:

Ataques de Intercepción (Sniffing): Un atacante conectado a la misma red puede capturar todo el tráfico en texto plano que emite tu dispositivo.

Ataques Man-in-the-Middle (MitM): Si el sitio utilizara formularios de inicio de sesión por HTTP, las credenciales (usuario y contraseña) viajarían legibles, permitiendo que un atacante las robe instantáneamente.

Secuestro de Sesión (Session Hijacking): Si las cookies de autenticación no poseen la etiqueta Secure, un atacante puede capturarlas del encabezado HTTP y suplantar la identidad de la víctima en aplicaciones web.

Inyección de Código (Modificación de Contenido): En redes maliciosas, un atacante operando un proxy transparente podría inyectar scripts maliciosos (XSS) o malware directamente en el flujo HTML que responde el servidor HTTP.

5. El Rol de una VPN en la Mitigación (Respuesta 4)
Implementar una Red Privada Virtual (VPN) cambia radicalmente el escenario de seguridad frente a redes hostiles:

Cifrado Robusto: Todo el tráfico generado por el equipo es encapsulado y cifrado mediante algoritmos avanzados (como AES-256 o ChaCha20) antes de abandonar el dispositivo.

Túnel Seguro: Se establece un túnel virtual cifrado entre el equipo del usuario y el servidor de la VPN. Para el router de la red Wi-Fi pública, el destino final del tráfico deja de ser el sitio web real y pasa a ser únicamente la IP del servidor VPN, volviendo el contenido ilegible ("basura binaria" aparente).

Privacidad y Ocultamiento de Tráfico: El administrador de la red pública o un atacante en el aire no pueden ver qué sitios web estás visitando (URL, métodos, headers ni payloads), solo sabrán que estás enviando paquetes cifrados hacia una dirección IP externa.

6. 3 Reglas de Oro para Navegar en Redes Wi-Fi Públicas (Respuesta 5)
Prioriza siempre HTTPS: Asegúrate de que las plataformas que utilices fuercen conexiones cifradas mediante certificados SSL/TLS válidos (y utiliza extensiones como HTTPS-Everywhere o el modo HTTPS-Only de tu navegador).

Conéctate a través de una VPN de confianza: Utiliza un servicio de VPN verificado siempre que te conectes a redes inalámbricas abiertas o no confiables para blindar todo tu tráfico frente a ataques de escucha local.

Evita transacciones críticas en redes abiertas: No realices operaciones bancarias, acceso a portales corporativos sensibles ni introduzcas credenciales personales en redes públicas a menos que cuentes con un túnel VPN activo y verificado.
