# Recopilación de información y planificación de estrategias de ataque

### Introducción
Aprendimos en el capítulo anterior los conceptos básicos de la caza de subdominios. En este capítulo, profundizamos un poco más y analizamos otras herramientas diferentes disponibles para reunir Intel en nuestro objetivo. Comenzamos usando las infames herramientas de Kali Linux.
La recopilación de información es una etapa muy crucial en la realización de una prueba de penetración, ya que cada paso siguiente que demos después será totalmente el resultado de toda la información que recopilemos durante esta etapa. Por eso es muy importante que recopilemos la mayor cantidad de información posible antes de pasar a la etapa de explotación.
### Obtener una lista de subdominios
No siempre tenemos una situación en la que un cliente ha definido un alcance completo y detallado de lo que necesita ser probado. Por lo tanto, utilizaremos las recetas mencionadas a continuación para recopilar tanta información como podamos para realizar un pentest.
### Fierce
Comenzamos con saltando a la Terminal de Kali y usando la primera y la más herramienta ampliamente utilizada feroz.
### Cómo hacerlo...

Los siguientes pasos demuestran el uso de fierce:

1.     Para  iniciar fierce,  escribimos  fierce -h  para  ver el menú de ayuda:

![](img/fierceh.png)

1. Para realizar un escaneo de subdominio usamos el siguiente comando:
	`fierce --domain host.com --connect`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/fiercesd.png)

### DNSdumpster
Este es un proyecto gratuito de Hacker Target para buscar subdominios. Se basa en https://scans.io/ para sus resultados. También se puede utilizar para obtener los subdominios de un sitio web. Siempre deberíamos preferir usar más de una herramienta para la enumeración de subdominios, ya que podemos obtener algo de otras herramientas que la primera no pudo seleccionar.
### Cómo hacerlo...
Es bastante sencillo de utilizar. Escribimos el nombre de dominio para el que queremos los subdominios y nos mostrará los resultados.

![](img/dnssunpster.png)

### Usar Shodan para divertirse y obtener ganancias
Shodan es el primer motor de búsqueda del mundo que busca dispositivos conectados a Internet. Fue lanzado en 2009 por John Matherly. Shodan se puede utilizar para buscar cámaras web, bases de datos, sistemas industriales, videojuegos, etc. Shodan recopila principalmente datos sobre los servicios web más populares en ejecución, como HTTP, HTTPS, MongoDB, FTP y muchos más.
### Preparándose
Para utilizar Shodan necesitaremos crear una cuenta en Shodan.
### Cómo hacerlo...
Para obtener más información sobre Shodan, siga los pasos indicados:
1. Abra su navegador y visite https://www.shodan.io:

![](img/shodanio.png)

2.     Comenzamos realizando una búsqueda simple de los servicios FTP en ejecución.Para hacer esto     nosotros podemos  usar los siguientes  Shodan  dorks: puerto:"21".La siguiente captura de pantalla muestra los resultados de  la búsqueda:

![](img/port21.png)

3.     Esta búsqueda puede hacerse más específica especificando un país/organización en particular:   puerto:"21" país:"IN".La  siguiente      captura de pantalla  muestra los    resultados de la búsqueda:
![](img/puertopais.png)

3.     Ahora podemos     ver todos los servidores FTP ejecutándose en la India; también podemos ver los servidores que permiten el inicio de sesión anónimo y la versión del servidor FTP que están ejecutando.

4.     A continuación,  probamos  el filtro de organización. Se puede hacer escribiendo puerto:"21" país:"IN" org:"BSNL" como se muestra en la siguiente captura de pantalla:

![](img/pco.png)

_Shodan tiene otras etiquetas también que pueden usarse para   realizar búsquedas avanzadas,  tales   como:_
_**net**:  para escanear IP rangos_ 
_**ciudad**:    para filtrar  por ciudad_

_Más    detalles pueden encontrarse en_  [_https://www.shodan.io/explore_](https://www.shodan.io/explore)

# Shodan  HoneyScore
Shodan Honeyscore es otro gran proyecto integrado en Python. Nos ayuda a determinar si una dirección IP que tenemos es un honeypot o un sistema real.

**Cómo hacerlo...**
Los siguientes pasos demuestran el uso de Shodan Honeyscore:

1.     Para   utilizar Shodan Honeyscore visitamos    [https://honeyscore.shodan.io/](https://honeyscore.shodan.io/):
![](img/honeyscore.png)

2.     Introduce  la  dirección IP que queremos comprobar y ¡listo!
![](img/honeyscoreip.png)

# Shodan  plugins

Para hacernos la vida aún más fácil, Shodan tiene complementos para Chrome y Firefox que se pueden usar para comprobar los puertos abiertos de los sitios web que visitamos mientras viajamos.

**Cómo hacerlo...**
Descargamos e instalamos el complemento desde   [https://www.shodan.io/](https://www.shodan.io/). Navega por cualquier sitio web y veremos que al hacer clic en el complemento podemos ver los puertos abiertos:

![](img/clip_image014.jpg)

### Usando Nmap para encontrar puertos abiertos
Network Mapper (Nmap) es un escáner de seguridad escrito por Gordon Lyon. Se utiliza para encontrar hosts y servicios en una red. Salió por primera vez en septiembre de 1997. Nmap tiene varias funciones, así como scripts para realizar diversas pruebas, como encontrar el sistema operativo, la versión del servicio, inicios de sesión predeterminados de fuerza bruta, etc.
Algunos de los tipos de exploración más comunes son:
- Escaneo de conexión TCP ()
- Escaneo sigiloso SYN
- escaneo UDP
- escaneo de ping
- Escaneo inactivo
### How  to  do it...

The     following  is the recipe for using  Nmap:

1.     Nmap is already installed  in Kali Linux. We can type the  following command to start   it          and     see      all        the      options  available:  `nmap -h`

The following      screenshot   shows  the  output  of the   preceding     command:
![](img/clip_image0031.png)

2.     Para realizar un escaneo básico utilizamos el siguiente comando:  `nmap -sV -Pn x.x.x.x`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/clip_image0061.png)

3.     `-Pn`   implica que no comprobamos si el host está activo o no realizando primero una solicitud de ping. El parámetro `-sV` es para enumerar todos los servicios en ejecución en los puertos abiertos encontrados.

4.     Otro indicador que podemos usar es `-A`, que realiza automáticamente la detección del sistema operativo, la detección de versiones, el escaneo de secuencias de comandos y el traceroute. El comando es: `nmap -A -Pn x.x.x.x`

5.     Para escanear un rango de IP o varias IP, podemos usar este comando: `nmap -A -Pn x.x.x.0/24`
### Usando scripts
El  **Nmap Scripting Engine** (**NSE**) permite  a los  usuarios  crear sus propios scripts para realizar   diferentes tareas   automáticamente. Estos scripts se ejecutan uno al lado del otro cuando se ejecuta un escaneo. Se pueden utilizar para realizar una detección de versiones más efectiva, explotar la vulnerabilidad, etc. El comando para usar  un script es: `nmap -Pn -sV host.com --script dns-brute`

![](img/clip_image0091.png)

El resultado del comando anterior es el siguiente:

![](img/clip_image0111.png)

Aquí, el script dns-brute intenta recuperar los subdominios disponibles mediante fuerza bruta contra un conjunto de nombres de subdominios comunes.
### Bypassing   firewalls with  Nmap
La mayoría de las veces durante un pentest nos encontraremos con sistemas protegidos por firewalls o por **Sistemas de Detección de Intrusos** (**IDS**). Nmap proporciona diferentes formas de evitar estos IDS/firewalls para realizar escaneos de puertos en una red. En esta receta, aprenderemos algunas de las formas en que podemos evitar los cortafuegos.
### TCP    ACK   scan
El escaneo ACK (-sA) envía paquetes de confirmación en lugar de paquetes SYN, y el firewall no crea registros de paquetes ACK, ya que tratará los paquetes ACK como respuestas a paquetes SYN. Se utiliza principalmente para mapear el tipo de firewall que se utiliza.
### Cómo hacerlo...
El escaneo ACK se realizó para mostrar puertos filtrados y sin filtrar en lugar de los abiertos.

El comando para escanear ACK es: `nmap -sA x.x.x.x`

Veamos la comparación de en qué se diferencia un escaneo normal de un escaneo ACK:

![](img/clip_image0141.png)

Aquí vemos la diferencia entre un escaneo normal y un escaneo ACK:

![](img/clip_image016.png)
### Cómo funciona...
Los resultados del análisis de los puertos filtrados y sin filtrar dependen de si el firewall utilizado tiene o no estado. Un cortafuegos con estado comprueba si un paquete ACK entrante forma parte de una conexión existente o no. Lo bloquea si los paquetes no forman parte de ninguna conexión solicitada. Por lo tanto, el puerto aparecerá como filtrado durante un escaneo.

Mientras que, en el caso de un firewall sin estado, no bloqueará los paquetes ACK y los puertos aparecerán sin filtrar.
### TCP    Window scan
El escaneo de ventana    (-sW)    es casi igual  que  un escaneo  ACK excepto   que muestra puertos abiertos y cerrados.
### Cómo hacerlo...
Veamos la diferencia entre un escaneo normal y un escaneo TCP:

1.     El comando a ejecutar es: `nmap -sW  x.x.x.x`
2.     Veamos  la comparación de  en qué   un escaneo  normal difiere de un escaneo de Windows TCP:

![](img/clip_image017.png)

3.     Podemos ver  la diferencia entre los      dos escaneos  en la  siguiente captura de pantalla:

![](img/clip_image019.png)
### Idle    scan
El escaneo inactivo es una técnica avanzada en la que ningún paquete enviado al objetivo puede rastrearse hasta la máquina atacante. Requiere que se especifique un host zombi.
### Cómo hacerlo...
El comando para realizar un análisis inactivo es: `nmap -sI zombiehost.com dominio.com`
### Cómo funciona...
El escaneo inactivo funciona sobre la base de un IPID predecible o un ID de fragmentación de IP del host zombie. Primero, se verifica el IPID del host zombie y luego se falsifica una solicitud de conexión desde ese host al host de destino. Si el puerto está abierto, se envía una confirmación al host zombie que restablece (RST) la conexión, ya que no tiene historial de apertura de dicha conexión. A continuación, el atacante vuelve a comprobar el IPID del zombi; si ha cambiado en un paso, implica que se recibió un RST del objetivo. Pero si el IPID ha cambiado en dos pasos, significa que el host zombie recibió un paquete desde el host de destino y hubo un RST en el host zombie, lo que implica que el puerto está abierto.
### Buscando directorios abiertos
En la receta anterior, analizamos cómo encontrar puertos abiertos en una IP de red o un nombre de dominio. A menudo vemos desarrolladores ejecutando servidores web en diferentes puertos. En ocasiones los desarrolladores también pueden dejar directorios mal configurados que pueden contener información jugosa para nosotros. Ya hemos cubierto `dirsearch` en el capítulo anterior; Aquí veremos alternativas.
### La herramienta dirb
La herramienta dirb es una herramienta bien conocida que se puede utilizar para abrir directorios por fuerza bruta. Aunque generalmente es lento y no admite subprocesos múltiples, sigue siendo una excelente manera de encontrar directorios/subdirectorios que pueden haberse dejado abiertos debido a una mala configuración.
### Cómo hacerlo...
Escriba el siguiente comando para iniciar la herramienta: `dirb https://dominio.com`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/dirb.png)
### Hay más...
También hay otras opciones en `dirb` que resultan útiles:
 - `-a`: para especificar un agente de usuario
- `-c`: para especificar una cookie
- `-H`: para ingresar un encabezado personalizado
- `-X`: para especificar la extensión del archivo
### Realizando magia profunda con DMitry
La herramienta de recopilación de información Deepmagic (DMitry) es una aplicación de código abierto de herramienta de línea de comandos codificada en C. Tiene la capacidad de recopilar subdominios, direcciones de correo electrónico, información whois, etc., sobre un objetivo.
### Cómo hacerlo...
Para obtener más información sobre DMitry, siga los pasos indicados:
1. Usamos un comando simple: `dmitry -h`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/dmitry1.png)

1. A continuación, intentamos realizar un correo electrónico, whois, escaneo de puerto TCP y búsqueda de subdominio usando lo siguiente: `dmitry -s -e -w -p dominio.com`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/dmitry2.png)

![](img/dmitry3.png)
### Buscando fallas SSL
La mayoría de las aplicaciones web actuales utilizan SSL para comunicarse con el servidor. SSLSCAN es una gran herramienta para verificar SSL en busca de fallas o configuraciones incorrectas.
### Cómo hacerlo...
Para obtener más información sobre sslscan, siga los pasos indicados:
1. Miraremos el manual de ayuda para ver las diversas opciones que tiene la herramienta: `sslscan -h`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/sslscan1.png)

1. Para ejecutar la herramienta contra un host, escribimos lo siguiente: `sslscan host.com:port`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/sslscan2.png)
### Explorando conexiones con intrace
La herramienta Intrace es una gran herramienta para enumerar saltos de IP en conexiones TCP existentes. Puede resultar útil para eludir el firewall y recopilar más información sobre una red.
### Cómo hacerlo...
Ejecute el siguiente comando: `intrace -h	hostname.com -p	port -s	sizeofpacket`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/intrace1.png)

### Profundizando con la theharvester
La herramienta theharvester es una gran herramienta para realizar pruebas de penetración ya que nos ayuda a encontrar mucha información sobre una empresa. Se puede utilizar para buscar cuentas de correo electrónico, subdominios, etc. En esta receta, aprenderemos cómo usarlo para descubrir datos.
### Cómo hacerlo...
El comando es bastante simple: `theharvester -d domain/name -l 20 -b all`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/theharvester1.png)

### Cómo funciona...
En la receta anterior, -d es para el nombre de dominio o la palabra clave que queremos buscar, -l es para limitar el número de resultados de búsqueda y -b es la fuente que queremos que utilice la herramienta mientras recopila información. La herramienta es compatible con fuentes de Google, Google CSE, Bing, Bing API, PGP, LinkedIn, Google Profiles, people123, Jigsaw, Twitter y Google Plus.
### Encontrar la tecnología detrás de las aplicaciones web
No tiene sentido iniciar un pentest en una aplicación web sin saber cuál es la tecnología real detrás de ella. Por ejemplo, sería absolutamente inútil ejecutar dirsearch para buscar archivos con la extensión .php cuando la tecnología en realidad es ASP.NET. Entonces, en esta receta, aprenderemos a usar una herramienta simple, whatweb, para comprender la tecnología detrás de una aplicación web. Viene por defecto en Kali.
También se puede instalar manualmente desde la URL https://github.com/urbanadventurer/WhatWe b. El uso de `whatweb` se puede realizar de la siguiente manera:
1. La herramienta se puede iniciar usando el siguiente comando: `whatweb`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/whatweb1.png)

1. El nombre de dominio se puede proporcionar como parámetro, o se pueden ingresar varios nombres de dominio usando un argumento `--input-file`: `whatweb hostname.com`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/whatweb2.png)

### Escaneando IP con Masscan
La herramienta Masscan es una herramienta asombrosa; Es la herramienta de escaneo de puertos más rápida. Se supone que escanea todo Internet cuando transmite a una velocidad de 10 millones de paquetes por segundo. Es una buena alternativa a Nmap cuando sabemos exactamente qué puertos buscamos en una red.
Es similar a Nmap, sin embargo, en que no admite el escaneo de puertos predeterminados; todos los puertos deben especificarse usando `-p`.
La herramienta Masscan es fácil de usar. Podemos comenzar un escaneo de una red usando el siguiente comando: `mascan 192.168.1.0/24 -p 80,443,23`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/msscan1.png)

También podemos especificar la velocidad del paquete usando `--max-rate`. De forma predeterminada, la velocidad es de 100 paquetes por segundo. No se recomienda su uso ya que supondrá una gran carga para el dispositivo de red.
### Husmeando con Kismet
Kismet es un detector de redes inalámbricas de capa 2. Resulta útil porque al realizar el pentest en un entorno corporativo, es posible que necesitemos buscar también redes inalámbricas. Kismet puede detectar el tráfico 802.11a/b/g/n. Funciona con cualquier tarjeta inalámbrica que admita modos de monitoreo sin formato.
En esta receta, aprenderemos cómo usar Kismet para monitorear redes Wi-Fi.
Para obtener más información sobre Kismet, siga los pasos indicados:
1. Usamos el siguiente comando para iniciar Kismet: `kismet`
La siguiente captura de pantalla muestra el resultado del comando anterior:

![](img/kismet1.png)

