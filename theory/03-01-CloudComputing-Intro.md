# 3.1 De la virtualización a la nube

* La virtualización es una capa de abstracción sobre Hardware físico que nos permite dividir dichos recursos físicos (e.g., procesador, memoria o almacenamiento) en múltiples unidades ***virtuales*** con las que se pueden operar como si fuera Hardware independiente.

* Por ejemplo, esto nos permite generar en un solo ordenador varias ***máquinas virtuales*** (VMs del inglés *virtual machines*) que se comportan como ordenadores completamente independientes con una realidad física.

  | | Instalación clásica de servidor | Instalación de servidor virtualizado |
  |---|---|---|
  | Capa superior | `APPLICATION` (una única aplicación) | `APP` / `OS` por cada VM (varias, una por bloque) |
  | Capa intermedia | `OPERATING SYSTEM` | `VMware ESX` (hipervisor) |
  | Capa base | Hardware físico | Hardware físico |

* Los tipos de virtualización más populares son:

  * Virtualización de procesamiento (Server Virtualisation)
  * Virtualización de almacenamiento (Storage Virtualisation)
  * Virtualización de redes (Network Virtualisation)
  * Virtualización de sistemas operativos (Containerisation)

* ¿Qué es la nube (*cloud*) entonces, y qué tiene que ver con todo esto? En pocas palabras, la virtualización es la tecnología facilitadora, y la nube es el entorno donde se extraen, agrupan y comparten recursos. Así pues, la nube se suele definir como:

  > *Un conjunto de software y servicios que permiten al desarrollador centrarse en el proyecto de desarrollo en lugar de en la infraestructura necesaria*
  >
  > J.J. Geewax, Google Cloud Platform in Action

* Pero, la nube no es simplemente virtualización. La nube conlleva la posibilidad de acceder a los recursos virtuales creados con la virtualización a través de redes privadas o públicas. Esta posibilidad conlleva, evidentemente, la necesidad de un conjunto de software y servicios que permiten su funcionamiento y gestión por parte de tanto el proveedor (*cloud provider*) como el usuario (*cloud consumer*). Este ecosistema de software y servicios suele seguir la siguiente estructura por capas:

  | Capa | Contenido |
  |---|---|
  | **Servicios** | Infrastructure as a Service (Server/Desktop/Storage/Network Cloud) · Platform as a Service (Middleware, Database, Java Runtime, Development Tooling, Web 2.0 App Runtime) · Software as a Service (Business Processes, Collaboration, Industry Applications, CRM/ERP/HR) |
  | **Cloud Platform — Business Support System** | Billing/Pricing · Reporting · Order Management · Contracts Management · SLA Management · Account Management |
  | **Cloud Platform — Operational Support System** | Infrastructure Management · Capacity Planning · Infrastructure Security · Metering · Monitoring · Provisioning |
  | **Base** | Virtualized Hardware · Storage Resource Pool · Network Device Infrastructure |

* Como se puede intuir del punto anterior, en el mundo cloud se pueden identificar ciertos "roles" característicos que son universales, como son por ejemplo:

  * Proveedor Cloud (Cloud Provider):
    * La compañía/organización que provee la infraestructura tecnológica cloud
    * El proveedor cloud es responsable del mantenimiento de la infraestructura así como del cumplimiento con los acuerdos de disponibilidad (SLA, del inglés *Service-Level Agreement*) con el consumidor
  * Cliente Cloud (Cloud Consumer):
    * Es la compañía/organización/persona que firma un acuerdo con el cloud provider para usar los servicios IT ofertados por el proveedor.
    * Dentro de esta organización conviven, entre otros, los dos equipos siguientes: Arquitectura y Desarrollo.
  * Equipo de Arquitectura Cloud (Cloud Architect):
    * Es el equipo encargado de sentar las bases técnicas y de gobierno con las que la empresa va a operar en el nuevo proveedor cloud, normalmente mediante un primer proyecto llamado Landing Zone. Esto abarca: jerarquía de recursos, nomenclatura, redes, seguridad, automatización, organización interna, monitorización y alertado, integrándose con los sistemas ya existentes.
    * Este trabajo de gobierno es el que permite que, a partir de ahí, el resto de equipos (empezando por Desarrollo) puedan operar con autonomía y seguridad dentro del proyecto/cuenta cloud.
  * Equipo de Desarrollo (Dev Teams):
    * Son los equipos que, dentro del marco ya definido por Arquitectura, consumen los servicios IT del proveedor cloud para construir, desplegar y operar sus propias aplicaciones.
  * Operación/Administrador Cloud (Cloud Resource Administrator/Operator):
    * Es la compañía/organización/persona que se encarga de la administración de los servicios basados en la infraestructura cloud (incluyendo los propios servicios cloud ofertados por el proveedor).
    * Puede ser o no parte de la entidad consumidora, ya que podría tratarse de una compañía externa al consumidor que se ha contratado con el cometido de administrar los servicios creados por el consumidor en la infraestructura cloud.
    * Este rol no siempre es un equipo separado: en organizaciones DevOps-maduras es el propio equipo de Desarrollo quien opera lo que construye. En [3.1.1](#311-prácticas-ágiles-de-trabajar-en-el-cloud) vemos justamente cómo se organiza esa responsabilidad de operación (DevOps, SRE, Platform Engineering).
  * Seguridad (Cloud Auditor/Security):
    * Es una compañía/organización independiente (normalmente acreditada) que lleva a cabo revisiones regulares en relación a controles de seguridad, privacidad y continuidad de negocio.
    * El objetivo principal de este rol es el de generar un informe exhaustivo e independiente sobre el entorno cloud que ayude a identificar vulnerabilidades y puntos débiles, que habrán de ser subsanados en un plazo determinado, para fortalecer la relación de confianza entre el consumidor y el proveedor cloud.
  * Finanzas:
    * Es el departamento encargado de controlar el gasto en cloud. Este departamento suele haber gente de los equipos de Operación Cloud que conocen los detalles de la facturación para ser capaces de justificar el gasto en las distintas partidas.
    * La evolución es el concepto de FINOPS: es una práctica que se centra en la gestión eficiente de los costos en la nube y en entornos de tecnología de la información en general. Su objetivo principal es ayudar a las empresas a optimizar sus gastos en la nube.

* Normalmente, todo proveedor cloud ofrece una interfaz gráfica muy accesible y agradable para el usuario, así como interfaces programáticas (APIs) que permiten la automatización de tareas repetitivas.

## 3.1.1 Prácticas ágiles de trabajar en el cloud

DevOps, SRE (Site Reliability Engineering) y Platform Engineering **no son tres alternativas al mismo nivel** entre las que una empresa elige una sola, como si fueran sabores distintos de lo mismo. Son más bien **tres capas que se apoyan una en otra**: una filosofía, una forma concreta de llevarla a la práctica con métricas, y una forma de escalar esa práctica cuando hay muchos equipos.

### DevOps (Desarrollo y Operaciones)

*Enfoque*: DevOps es, ante todo, una **filosofía cultural**, no un equipo con un manual de instrucciones concreto: busca derribar el muro entre quien desarrolla y quien opera, de manera que quien construye el software también se responsabilice de que funcione en producción ("*you build it, you run it*").

*Responsabilidades*: automatizar el ciclo de vida completo del software (codificación, integración, despliegue, monitorización), apoyándose en infraestructura como código (IaC) y en CI/CD.

*Objetivo*: reducir el tiempo entre escribir código y tenerlo en producción, sin sacrificar calidad ni estabilidad.

### SRE (Site Reliability Engineering)

*Enfoque*: SRE, nacida en Google, es una **implementación concreta y bastante prescriptiva** de la filosofía DevOps. Como dice el propio libro de SRE de Google: *"class SRE implements interface DevOps"*. Su aportación diferencial es medir la fiabilidad en vez de darla por sentada:

- **SLI** (*Service Level Indicator*): una métrica de fiabilidad (p.ej. % de peticiones respondidas en menos de 200ms).
- **SLO** (*Service Level Objective*): el objetivo sobre esa métrica (p.ej. 99.9% al mes).
- **Error budget**: el margen de fallo que te queda antes de incumplir el SLO. Mientras hay margen, el equipo prioriza velocidad y nuevas *features*; cuando se agota, se prioriza estabilidad y se congelan lanzamientos.

*Responsabilidades*: automatización de tareas operativas, reducción del *toil* (trabajo manual repetitivo, típicamente acotado a un máximo del tiempo del equipo), *postmortems* sin buscar culpables (*blameless*), y gestión activa del error budget.

*Objetivo*: que la fiabilidad sea una decisión de ingeniería medible, no una sensación.

⚠️ Matiz importante: SRE **no es "tirarle la operación a otro equipo"**. Quien desarrolla el servicio sigue de guardia; un equipo de SRE solo asume la operación de un servicio si este cumple unos requisitos mínimos de fiabilidad y observabilidad, y puede devolver esa responsabilidad al equipo de desarrollo si el error budget se agota sistemáticamente. Es una relación con criterios de entrada y salida, no un *handoff* sin más.

### Platform Engineering

*Enfoque*: Platform Engineering aparece cuando el modelo "cada equipo es dueño de su propio DevOps/SRE" deja de escalar: con decenas o cientos de equipos, cada uno acaba reinventando su propio pipeline de CI/CD, su propio cluster, su propia observabilidad... con el consiguiente coste y falta de estandarización.

*Responsabilidades*: un equipo de plataforma construye y mantiene una **plataforma interna de autoservicio** (*Internal Developer Platform*, IDP) con "caminos asfaltados" (*golden paths*): plantillas, *pipelines* y herramientas ya integradas y con las buenas prácticas de seguridad/observabilidad aplicadas por defecto.

*Objetivo*: que el resto de equipos conserve la autonomía y velocidad que promete DevOps, pero sin que cada uno necesite ser experto en infraestructura, reduciendo así la carga cognitiva de cada equipo de producto.

### Resumen

| | DevOps | SRE | Platform Engineering |
|---|---|---|---|
| **Qué es** | Una cultura/filosofía | Una disciplina de ingeniería que la implementa con métricas | Una disciplina que la escala construyendo una plataforma |
| **Mecanismo clave** | Automatización + responsabilidad compartida | SLI/SLO + error budget | Self-service + *golden paths* |
| **¿Quién opera el servicio?** | Quien lo construye | Quien lo construye, con soporte de SRE si cumple el SLO | Quien lo construye, apoyándose en la plataforma común |

En la práctica, las tres conviven: una organización con cultura DevOps puede tener un equipo de SRE que aplique el rigor de los error budgets a sus servicios más críticos, y un equipo de Platform Engineering que le dé a todos los demás equipos las herramientas para trabajar así sin fricción.
