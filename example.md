# CISCO

**ISE**

Endpoint profile policy: Define los atributos que debe coincidir para que un dispositivo se clasifique como ese tipo de terminal.

Cisco crea cinco grupos Endpoint Identity por defecto:

1. Blacklist
2. Guest Endpoints
3. Profiled
4. Registered services
5. Unknow

Personas (Responsabilidades a escala): Cada persona tiene una función diferente dentro de una implementación de cisco ISE. Las personas se ejecutan dentro de los nodos de ISE.

Nodo ISE: Dispositivo individual, puede ser virtual o físico.

Tipos de personas:

1. Administration
2. Monitoring
3. Policy Service
4. PxGrid

Administration (Persona más importante): Configure and administer the network security policy.

- PAN (Policy Administration Node) - incluye la configuración de las licencias.

Monitoring (Persona de supervisión): Actua como un servidor de registro centralizado.

- MnT (Monitoring and Troubleshooting Node) - Supervisión y resolución de problemas - puede existir hasta 2 Mnt en un cube ISE.

Policy Service (Persona que actua como un Radius):

- PSN (Policy Service Node) - no necesita de PAN para las autenticaciones. El CoA (Change of Authorization) es creado por el PSN. El PSN fuerza la reautenticación.

  Servicios encontrados: Profiling of endpoints, TC-NAC (Threat Centric Network Access Control), SGT Exchange Protocol, TACACS+ ---- puede existir hasta 50 PSN en un cube ISE.

- PxGrid: Se encarga de compartir datos de seguridad de manera eficiente y escalable 

Posture: Evalua el estado final de un punto final.

Puertos utilizados para la CoA: 2799, 1700

NAD: Network Access Device
