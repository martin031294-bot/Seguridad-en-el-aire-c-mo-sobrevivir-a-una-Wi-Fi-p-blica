# Seguridad-en-el-aire-c-mo-sobrevivir-a-una-Wi-Fi-p-blica
Trabajo Practico 6
1. Introducción
El presente informe documenta el análisis de tráfico y riesgos asociados a la navegación web mediante redes públicas o Wi-Fi no cifradas. El objetivo de este ejercicio es identificar las vulnerabilidades derivadas del uso de protocolos en texto plano (HTTP) y fundamentar las medidas de mitigación mediante tecnología VPN y mejores prácticas de ciberseguridad.
2. Sitio Analizado y Evidencia Observada
Durante la prueba de concepto realizada en el entorno de pruebas, se inspeccionó la navegación hacia un host deliberadamente inseguro mediante herramientas de desarrollador (Developer Tools).
URL solicitada: `http://neverssl.com`
Host visitado: `http://ejemplo-inseguro.com` (Host de prueba identificado en la captura de tráfico)
Método HTTP: `GET`
Protocolo utilizado: `HTTP/1.1` (Sin cifrado TLS/SSL)
Headers/User-Agent visibles: Se observaron en texto claro los encabezados de petición, incluyendo `Host`, `User-Agent` (navegador y sistema operativo), `Accept-Language` y métodos de solicitud.
3. Riesgos Encontrados
El sitio analizado utiliza HTTP en lugar de HTTPS. Al navegar mediante HTTP en una red Wi-Fi pública, toda la información viaja en texto plano a través del espectro radioeléctrico.
Los principales riesgos identificados incluyen:
Intercepción de datos (Sniffing): Cualquier atacante conectado a la misma red puede capturar los paquetes de datos utilizando analizadores de red (como Wireshark) y leer URLs, cookies de sesión, credenciales o formularios en texto claro.
Ataques de Intermediario (Man-in-the-Middle - MitM): Un tercero puede alterar el contenido de las páginas solicitadas en tiempo real, inyectando scripts maliciosos o redirigiendo al usuario a sitios fraudulentos.
Redes Gemelas Malignas (Evil Twins): Exposiciones a hotspots maliciosos creados para suplantar redes legítimas y recolectar información sensible.
4. Cómo Ayuda una VPN
La implementación de una Red Privada Virtual (VPN) transforma drásticamente la seguridad del escenario de navegación mediante los siguientes mecanismos:
Túnel Seguro y Encapsulamiento: La VPN crea un túnel de transmisión de datos encapsulado entre el dispositivo del usuario y el servidor VPN.
Cifrado de Extremo a Extremo: Toda la información que sale del dispositivo es procesada mediante cifrado fuerte antes de ser emitida a la red Wi-Fi pública.
Protección del Tráfico y Privacidad: Aunque un atacante interceptase los paquetes con herramientas como Wireshark o controlara un router malicioso (Evil Twin), únicamente observará un flujo ilegible de datos cifrados, manteniendo la confidencialidad del destino final y del contenido de la comunicación.
5. Las 3 Reglas de Oro para Redes Wi-Fi Públicas
Utilizar siempre una VPN y verificar HTTPS: Mantener el túnel VPN activo en todo momento al conectar el equipo a redes externas y cerciorarse de que las webs muestren el candado de seguridad (HTTPS).
Desactivar la conexión automática y el uso compartido: Configurar el dispositivo para no conectarse automáticamente a redes abiertas y deshabilitar el intercambio de archivos o carpetas públicas en el sistema operativo.
No realizar transacciones sensibles: Evitar acceder a la banca en línea, realizar compras con tarjeta de crédito o ingresar credenciales críticas mientras se esté conectado a una Wi-Fi pública.
