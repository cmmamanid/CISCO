# CISCO

**ISE**

**Posture:** Evalua el estado final de un punto final.

**Puertos utilizados para la CoA:** 2799, 1700

**NAD:** Network Access Device



## PARTE 1 : AUTHENTICATION, AUTHORIZATION AND ACCOUNTIG

#### CHAPTER 1: Fundamentals of AAA

La Administración de dispositivos puede ser de manera muy interactiva.

Terminal Access Controller Access Control system (TACACS)

Remote Authentication Dial-In User Services (RADIUS)

**Authentication**: Asegurarse de saber quien es realmente esa entidad.

**Authorization**: Asegurarse  que la entidad este autorizada para realizar dicha acción.

**Accounting**: Mantener un registro de los cambios que realiza.

​		Ejemplo: Utilización de  tarjeta de crédito:

​						Authentication: Verificar la identidad del usuario de la tarjeta.

​						Authorization: Validar que la persona que porta la tarjeta tenga coincidencia de su 						nombre con la del propietario de la tarjeta.

​						Accounting: Registro de las acciones realizadas con la tarjeta



**TACACS**: Permite autorizar y autenticar, este permite separar la autorización de AAA, lo que permite autenticar una vez y realizar multiples autorizaciones.

- TCP 49
- Encriptación payload
- Separa autenticación y autorización
- Device Administration

**RADIUS**: No permite controlar que comandos se pueden ejecutar.

- UDP 1812, 1813 - 1645, 1646
- Encriptación de solo password
- Combina autenticación y autorización
- Network Access

**AV Pairs**: Atributo que se le asigna a la sesión de autenticación, el atributo y su valor se emparejan, por ejemplo: VLAN y su ID o ACL y su ACL-name.

**CoA**: Mejora de Radius conocida como extensiones de autorización dinámica de RADIUS, mas comunmente llamado Change of Authorization (COA).



#### CHAPTER 2: Indentity Management 

**Identity Stores**: Es basicamente una base de datos donde se almacenan las credenciales de los usuarios y endpoints. Puede estar en un base de datos interna o externa (AD, LDAP, etc).

**Internal User Identities**: Cisco ISE tiene un almacen de identidad interno para autenticar y autorizar, que se puede utilizar para un numero limitado de cuentas de usuario.

**External Identity Stores**: Permiten una mejor escalabilidad y gestión de los procesos de autorización y autenticación de ISE, así como la integración de otros servicios de autenticación. Cisco ISE se conecta a la fuente de identidad externa para verificar las credenciales de nombre de usuario y contraseña para las políticas de autenticación. La información de certificado también se puede recuperar de un almacén de identidades externo.

**External Identity Stores**: 

- Active Directory
- LDAP
- ODBC
- RADIUS Token
- RSA SecurID
- SAML Id Providers

1. Active Directory: Sigue la estructura X.500 al igual que DNS, AD aprovecha los dominios de AD, que son agrupaciones de usuarios y cuentas de máquinas, permisos y políticas. (AD-forest, AD-root domain, AD-child domain).

2. LDAP: Es un protocolo ligero de acceso a directorios (LDAP), se utiliza para conectarse a base de datos de servicios de directorio X.500 y recuperar información de ellas. No se usa muy a menudo con ISE, debido a que este tiene un conectar más poderoso. El uso de LDAP como almacén de identidad externo es compatible para autenticación de usuarios. TCP 389, se recomienda utilizar LDAP con SSL TCP 636.

   

#### CHAPTER 3: Extensive authentication Protocol (EAP) over LAN 802.1X

Extensive authentication 

Protocol EAP over LAN 802.1X

IEEE estandarizo 802.1X como una solución port base para el acceso a la red.

**Componentes**

1. Suplicant: Software del endpoint (tambien llamado peer) que se comunica con EAP en la capa 2, este software responde al autenticador y proporciona las credenciales.
2. Authenticator: Switch, WLC (NAD - Network Access Device) funcionan como middleman, encapsulan la comunicación dirigida al authentication server.
3. Authentication: Valida la identidad del endpoint y proporciona un resultado al Authenticator Server (ISE). 

**EAP Types:** 

1. Native EAP
2. Tunneled EAP: EAP nativo dentro de un tunnel TLS, entre el supplicant y el authenticator.

#### CHAPTER 4: Non-802.1X Authentication

Se mantiene debido a que no es práctico la autenticación de puertos por 802.1X, esto se refuerza con la utilización de dispositivos IoT, además muchos dispositivos IoT no son compatibles con 802.1X, por lo que debe existir otra forma de autenticar estos dispositivos. Esto tambien se debe aplicar para dispositivos temporales o usuarios invitados que necesitan acceso a internet.

**MAC Authentication Bypass**: Una solución es hacer que el authenticator actue en nombre del endpoint, el authenticator utiliza la dirección MAC del endpoint como identidad. (MAB) Se habilita despues de 3 intentos fallidos de 30s se acceso mediante 802.1X

Otro camino para mejorar la seguridad de MAB es combinar con profiling para autorizar un endpoint, con el profiling, ISE recolecta atributos acerca del dispositivo conectado para crear un huella digital, basada en información y el tipo del dispositivo que se esta conectando para garantizar que se le pueda otorgar autorización en la red.

**Web Authentication**: Autenticación de un endpoint que no tiene configurado un supplicant. El autenticador (conmutador) envía la solicitud del endpoint a un portal web local o centralizado, el nombre del usuario y la contraseña enviados al portal web se envían luego al servidor de autenticación ISE para su autenticación.

**Local Web Authentication**: El autenticador redirige el tráfico web (HTTP/HTTPS) a un portal web alojado localmente, donde un usuario puede ingresar usuario y contraseña. El autenticador (conmutador) envía la solicitud e acceso al servidor de autenticación. Cada vez que el conmutador envía la credenciales del usuario, el proceso se considera LWA. No soporta policy acceptance pages, client provisioning,  password changing, self-registratios o device registration, para usar estos servicios avanzados es necesario utilizar Centralized Web Authentication. Guest VLAN y LWA son mutuamente excluyentes, tampoco LWA soporta CoA, por lo que las políticas de acceso no pueden ser cambiadas basadas en posture o profiling state o por la necesidad de poner en cuarentena un endpoint.

**Local Web Authentication with a Centralized Portal**:  La utilización de un portal centralizado permite que una organización personalice el portal. Con los conmutadores de Cisco, las páginas web almacenadas localmente pueden contener la cadena de redireccionamiento que envía el tráfico web del usuario al portal alojado de forma centralizada.  CoA no funciona y el aprovisionamiento de clientes y otras funciones avanzadas tampoco están disponibles. Este método no se ha adoptado ni se utiliza de forma generalizada por estos motivos. 

**Centralized Web Authentication**: CWA es solo para usuarios interactivos que tienen navegadores web, las funciones de WebAuth y VLAN de invitado permanecen mutuamente excluyentes. CoA funciona completamente con CWA, lo que conduce a la compatibilidad con todos los resultados de autorización, como la autorización de ACL y VLAN. Cuando se usa CWA, normalmente no hay ningún suplicante en el punto final, por lo tanto, el portal debe usar un subprograma ActiveX o Java para manejar la renovación de la dirección IP después de asignar VLAN. CWA soporta servicios avanzados como client provisioning, posture assessments, acceptable use policies, password changing, self-registration y device registration.

**Centralized Web Authentication with Third-Party Network Device Support**: La versión 2.1 de ISE agregó soporte para dispositivos de acceso a la red de terceros, que incluían servicios DHCP y DNS. Dado que muchos dispositivos de red de terceros no admiten la redirección de URL estática o dinámica de forma nativa, esta importante mejora le dio a ISE la capacidad de proporcionar una VLAN de autenticación (o VLAN de autenticación, como se la denomina comúnmente) para simular ese flujo de redirección de URL.

**Remote-Access Connections**: Cableada, inalámbrica y VPN (IPsec o SSL).



#### CHAPTER 5: Introduction to advanced concepts

**Authorization**: Proceso para determinar a que recursos puede tener acceso un usuario autenticado.

**No CoA**: (default)puede usar esta opción para deshabilitar la configuración global de CoA. Esta configuración anula cualquier CoA configurado por política de creación de perfiles de punto final. Si el objetivo es solo la visibilidad, conserve el valor predeterminado como Sin CoA.

**Port Bounce**: puede usar esta opción si el puerto del conmutador existe con una sola sesión. Si el puerto existe con varias sesiones, utilice la opción Reautorizar. Si el objetivo es actualizar inmediatamente la política de acceso en función de los cambios de perfil, seleccione la opción Port Bounce, esto garantizará que todos los puntos finales sin cliente se vuelvan a autorizar y la dirección IP se actualice, si es necesario.

**Reauth**: puede utilizar esta opción para aplicar la reautenticación de un punto final ya autenticado cuando se crea un perfil. Seleccione la opción Reautorizar, si no se espera ningún cambio de dirección o VLAN después de la reautorización de la sesión actual. 

**Change Of Authorization**: Es un estándar RFC 5176, mecanismo para cambiar los atributos AAA de una sesión después de que se haya autenticado.

**Automating MAC Authentication Bypass (MAB)**: la omisión de autenticación MAC (MAB) es el proceso mediante el cual un punto final omite la autenticación utilizando solo su dirección MAC, esta solicitud de acceso utiliza la dirección MAC del punto final en los campos Identidad y Contraseña.

**Posture Assessment**: Es un proceso mediante el cual una aplicación (como el Módulo de postura Cisco AnyConnect ISE) que se ejecuta en un punto final o un archivo ejecutable temporal (como el Agente temporal de Cisco) que se ejecuta en el cliente proporciona información crítica sobre el software o sistema operativo que se está ejecutando activamente en el dispositivo. Se pueden comprobar varias condiciones como parte de la evaluación de la postura. Esta información sobre el punto final se envía al servidor de autenticación. El servidor compara los datos con la política de seguridad configurada y evalúa el dispositivo como Compliant, Non- Compliant y Unknown.

**Mobile Device Management (MDM)**: es un sistema de software de seguridad que permite a un administrador configurar y proteger un dispositivo móvil, independientemente de dónde esté ubicado. Como punto final inicialmente integrado con un administrador de dispositivos móviles, el propietario del punto final instala el software MDM y le da permiso para acceder al dispositivo y recopilar la información necesaria. El software MDM realiza una serie de evaluaciones en el dispositivo, identificando el estado actual de seguridad, software y redes, entre otros factores. Luego, esta información se pasa al servidor MDM para su procesamiento. Este servidor MDM puede residir en las instalaciones de la empresa o en la nube.



## PARTE 2: CISCO IDENTITY SERVICE ENGINE

#### CHAPTER 6: Cisco Identity Service Engine Architecture

**Endpoint profile policy:** Define los atributos que debe coincidir para que un dispositivo se clasifique como ese tipo de terminal.

Cisco crea cinco grupos Endpoint Identity por defecto:

1. Blacklist
2. Guest Endpoints
3. Profiled
4. Registered services
5. Unknow

**Personas** (Responsabilidades a escala): Cada persona tiene una función diferente dentro de una implementación de cisco ISE. Las personas se ejecutan dentro de los nodos de ISE.

**Nodo ISE:** Dispositivo individual, puede ser virtual o físico.

Tipos de personas:

1. Administration
2. Monitoring
3. Policy Service
4. PxGrid

**Administration** (Persona más importante): Configure and administer the network security policy.

- PAN (Policy Administration Node) - incluye la configuración de las licencias.

**Monitoring** (Persona de supervisión): Actua como un servidor de registro centralizado.

- MnT (Monitoring and Troubleshooting Node) - Supervisión y resolución de problemas - puede existir hasta 2 Mnt en un cube ISE.

**Policy Service** (Persona que actua como un Radius):

- PSN (Policy Service Node) - no necesita de PAN para las autenticaciones. El CoA (Change of Authorization) es creado por el PSN. El PSN fuerza la reautenticación.

  Servicios encontrados: Profiling of endpoints, TC-NAC (Threat Centric Network Access Control), SGT Exchange Protocol, TACACS+ ---- puede existir hasta 50 PSN en un cube ISE.

**PxGrid:** Se encarga de compartir datos de seguridad de manera eficiente y escalable.

**ISE Deployment Scenarios**

1. Single-Node Deployment: toda la infraestructura ISE reside en un solo dispositivo, una implementación de ISE de un solo nodo es responsable de realizar todas estas personas en un solo dispositivo, como no hay redundancia en esta solución y la disponibilidad de los recursos de la red puede verse afectada en caso de una interrupción.
2. Two-Node Deployment: Cisco ISE de dos nodos incorpora redundancia, que es muy recomendable en una red de producción. En este tipo de implementación, las diversas personas ISE se distribuyen en dos dispositivos, a veces se la denomina ISE distributed deployment. Las personas de Administración y Monitoreo tienen el concepto de nodos primarios y secundarios. Si ocurre una falla en el PAN primario, no ocurrirá sincronización entre el PAN y los PSN hasta que el PAN secundario se promueva a primario. Una vez que se convierte en principal, se puede reanudar la sincronización. A veces, esto se denomina "warm spare". Debido a que un PSN siempre está activo, cada NAD en la red debe apuntar a cada PSN. Si hay una falla de la persona de Policy Services (y, por lo tanto, el procesamiento de RADIUS) o una falla de un solo dispositivo, el NAD detecta la falla del servicio RADIUS en una de las PSN y dirige el 100% de las consultas RADIUS futuras desde ese NAD al PSN restante.
3. Distributed Deployments: Al separar la persona de Policy Services de las personas de administración y supervisión, las llamadas RADIUS a una PSN seguirán funcionando incluso si las personas de administración y supervisión fallan.

#### CHAPTER 7: A guided Tour of the Cisco ISE Graphical User Interface (GUI)

**Tipos de politicas ISE:** A medida que un Endpoint intenta tener acceso a la red mediante un NAD.

**Authentication:**  Capacidad de identificar un punto final o el usuario de un punto final cuando se conecta a la red.

**Authorization:** La concesión de accesos o la denegación.

**Profiling:** la creación de perfiles, es la capacidad de determinar el tipo de dispositivo que accede a la red.

**Posture**: Evaluación de la postura de un endpoint, incluido el sistema operativo y el software de seguridad complementario (antivirus, antimalware, antispyware, OS patches)

**Client Provisioning:** proceso mediante el cual todas las credenciales y configuraciones necesarias se implementan en un punto final, también se denomina onboarding. Algunos criterios: SO, NAD desde donde se conectan, método de acceso a la red wifi o cableado, etc.

**Trust Sec**: Es una solución de seguridad en la que se le asigna una etiqueta de grupo de seguridad (SGT) a un punto final después de la autenticación. Los SGT están diseñados para subdividir y distinguir fácilmente a los diferentes escenarios de usuario, por ejemplo, acceso completo vs invitado. cada paquete que tiene el mismo SGT, recibe el mismo nivel de acceso. El NAD inserta el SGT en cada paquete enviado por el punto final. La política TrustSec determina que SGT asignar a un punto final según el usuario del punto final, el tipo de punto final, el método de acceso y otros criterios que se pueden determinar a partir del proceso de autenticación.

#### CHAPTER 8: Initital Configuration of Cisco ISE

#### CHAPTER 9: Authentication Policies

#### CHAPTER 10: Authorization Policies



## PARTE 3: IMPLEMENTING SECURE NETWORK ACCESS

#### CHAPTER 11: Implement Wired and Wireless Authentication

#### CHAPTER 12: Web Authentication

#### CHAPTER 13: Guest Services

#### CHAPTER 14: Profiling



## PARTE 4: ADVANCED SECURE NETWORK ACCESS

#### CHAPTER 15: Certificate-Based Authentication

#### CHAPTER 16: Bring Your Own Device

#### CHAPTER 17: TrustSec and MACsec

#### CHAPTER 18: Posture Assessment



## PARTE 5: SAFELY DEPLOYING IN THE ENTERPRISE

#### CHAPTER 19: Deploying Safely

#### CHAPTER 20: ISE Scale and High Availability

#### CHAPTER 21: Troubleshooting Tools



## PARTE 6: EXTENDING SECURE ACCESS CONTROL

#### CHAPTER 22: ISE context sharing and remediation

#### CHAPTER 23: Threat Centric NAC



## PARTE 7: DEVICE ADMINISTRATION AAA

#### CHAPTER 24: Device Administration AAA with ISE

#### CHAPTER 25: Configuring Device Administration AAA with Cisco IOS

#### CHAPTER 26: Configuring Device Admin AAA with the Cisco WLC



