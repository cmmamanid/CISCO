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

**External Identity Stores**: Permiten una mejor escalabilidad y gestión de los procesos de autorización y autenticación de ISE, así como la integración de otros servicios de autenticación. Cisco ISE se conecta







#### CHAPTER 3: Extensive authentication Protocol (EAP) over LAN 802.1X

Extensive authentication 

Protocol EAP over LAN 802.1X

IEEE estandarizo 802.1X como una solución port base para el acceso a la red.

**Componentes**

1. Suplicant

#### CHAPTER 4: Non-802.1X Authentication

#### CHAPTER 5: Introduction to advanced concepts

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



