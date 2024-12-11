# REDES

[← Regresar a notas](../../README.md) <br>

---
> #### Red
> - Una <u>red</u> es un conjunto de dispositivos conectados entre sí con el propósito de compartir datos y recursos.
> - Una <u>subred</u> es una división lógica dentro de una red, diseñada para optimizar el tráfico de datos.
> - <u>Internet</u> es la red global que <u>conecta</u> millones de <u>redes</u> en todo el mundo.
>
> <img src="../resources/images/21-network/network.png" width="550" height="230">


> #### Protocolos de red
> Un protocolo de red es un conjunto de reglas y estándares que define cómo dos o más dispositivos intercambian información de manera fiable y estructurada a través de la red.
> - **HTTP / HTTPS**: Usado para la comunicación web.
> - **FTP**: Usado para la transferencia de archivos.
> - **SMTP**: Usado para el envío y recepción de correos electrónicos.
> - **TCP / IP**: Es la base para la comunicación en Internet.

> #### TCP (Transmission Control Protocol)
> - Permite conectar dos aplicaciones de manera <u>confiable</u>.
> - Crea un canal a través del cual cada una de las partes puede <u>enviar y recibir datos</u>.
> - Garantiza que los datos recibidos en ambos extremos sean íntegros y si esto no llegase a ocurrir, entonces reportará un error.

> #### Dirección IP
> Es un número que identifica de manera única un dispositivo dentro de una red. 
> 
> Versiones:
> - **IPv4**: Utiliza 32 bits (Ej. `192.168.1.1`). Es la versión más común.
> - **IPv6**: Utiliza 128 bits (Ej. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`). Soporta un mayor número de dispositivos conectados.
>
> Clasificación:
> - **Privadas**: Se utilizan dentro de redes locales y no son accesibles desde internet.
> - **Públicas**: Son únicas a nivel global y permiten que los dispositivos sean accesibles desde internet.
> 
> <img src="../resources/images/21-network/ip.png" width="700" height="300">

> #### Puerto
> Un puerto es un punto de acceso dentro de una computadora que permite redirigir los datos que llegan a través de una conexión de red hacia las aplicaciones o procesos que correspondan.
>
> <img src="../resources/images/21-network/port.svg" width="350" height="220">

> #### Socket
> Un socket es un punto de conexión único hacia un proceso o aplicación en toda la red, ya que especifica la dirección IP y el puerto. Por ejemplo, `192.168.0.1:8080`.

> #### Arquitectura de red cliente / servidor
> Describe cómo dos aplicaciones (cliente y servidor) interactúan en una red para intercambiar datos.
> - **Servidor**: Provee <u>servicios</u> al cliente.
> - **Cliente**: Consume los <u>servicios</u> que ofrece el servidor.

> #### Servicio
> Un servicio es un conjunto de <u>funcionalidades o recursos</u> que el servidor pone a disposición de las aplicaciones cliente.
> - **Solicitud (Request)**: El cliente envía una petición al servicio para recuperar datos o ejecutar una acción específica.
> - **Respuesta (Response)**: El servidor procesa la solicitud y envía una respuesta al cliente, proporcionando los resultados solicitados o confirmando que la acción se ha realizado.
>
> <img src="../resources/images/21-network/client-server.svg" width="750" height="300">
