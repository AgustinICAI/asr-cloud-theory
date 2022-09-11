# 3. Cloud Computing

### 3.5 Diseño y despliegue de aplicaciones nativas Cloud

Ahora que tenemos un buen conocimiento de lo que nos oferta una nube (bien sea pública o privada), vamos a proceder con un salto gradual desde el desarrollo local (típicamente monolítico) hasta el desarrollo nativo en nube (*cloud native*) en el que se aprovecharán todo el potencial ofertado por el *cloud computing*.

#### Aplicaciones nativas Cloud (Cloud native applications): Introducción

El concepto del desarrollo de **aplicaciones nativas cloud** hace referencia a un paradigma de desarrollo de software que utiliza el entorno cloud para crear y desplegar aplicaciones en infraestructuras dinámicas y flexibles, como es el caso de la nube. 

Este paradigma de desarrollo suele ir acompañado del uso de las siguientes tecnologías:

* Plataformas cloud
* Metodologías ágiles ([Agile software development](https://en.wikipedia.org/wiki/Agile_software_development))
* Contenerización y [microservicios](https://en.wikipedia.org/wiki/Microservices)
* Orquestación de contenedores ([Docker Compose](https://docs.docker.com/compose/) y [Kubernetes](https://en.wikipedia.org/wiki/Kubernetes) [k8s])
* Funciones (FaaS) y plataformas *serverless* ([Serverless computing](https://en.wikipedia.org/wiki/Serverless_computing))
* Integración continua y Entrega continua ([Continuos Integration and Continuos Delivery](https://en.wikipedia.org/wiki/CI/CD) [CI/CD])

<img src="/Users/mduranol/Dropbox/Root/Home/Documents/ICAI/course-2021/teaching/ASR/theory/images/cloud-native.png" alt="cloud-native" style="zoom:67%;" />



#### Contenerización y microservicios

Uno de las características fundamentales que diferencia una aplicación nativa cloud de una aplicación tradicional es precisamente la contenerización y su infraestructura de microservicios.

De la contenerización ya hemos hablado extendidamente en el capítulo anterior cuando tratamos la virtualización de sistemas operativos, tanto de ventajas como desventajas. Sin embargo, es bueno que subrayemos la importancia de dicha tecnología en lo que a la **reproducibilidad** se refiere. El contenerizar una aplicación con todas las dependencias requeridas ha revolucionado por completo el paradigma del desarrollo en servidores. Previamente a la contenerización, la estabilización de entornos de desarrollo podía llegar a ser algo bastante tedioso, incluso convertirse en un problema a la hora del poder desarrollar, llegando en los casos más extremos a  convertirse en un factor de entorpecimiento a la hora de llevar a producción nuevos desarrollos, por no ser compatibles estos con las dependencias instaladas en el entorno productivo, sobre todo en proyectos de larga envergadura. La contenerización ataca una de las caras de este problema y es el aislamiento de dependencias de una aplicación, lo cual hace posible que su desarrollo sea completamente reproducible en cualquier entorno de trabajo, bien sea testing, desarrollo o productivo.

La arquitectura basada en microservicios constituye otro cambio de paradigma en el desarrollo de software, y consiste en construir una aplicación como un conjunto de pequeños [servicios](https://es.wikipedia.org/wiki/Servicio_(arquitectura_de_sistemas)), los cuales se ejecutan en su propio [proceso](https://es.wikipedia.org/wiki/Proceso_(informática)) y se comunican con mecanismos ligeros (normalmente una [API](https://es.wikipedia.org/wiki/Interfaz_de_programación_de_aplicaciones) de [recursos HTTP](https://es.wikipedia.org/wiki/Hypertext_Transfer_Protocol)). Cada "micro"-servicio se encarga de implementar una funcionalidad completa de negocio, de manera independiente y completamente autónoma. Así, cada micro-servicio puede ser desplegado de forma independiente y puede estar programado en distintos lenguajes y usar diferentes tecnologías de almacenamiento de datos. Esta filosofía de desarrollo evidentemente rompe con la filosofía tradicional monolítica, orientada a poyectos, que no a funcionalidades. La filosofía monolítica conlleva una serie de restricciones bastante importantes a la hora del desarrollo, como es por ejemplo el hecho de forzar un único lenguaje de programación o compatibilidad de librerías para todo un proyecto, lo cuál se convierte en algo más y más complicado a medida que un proyecto crece en complejidad (lo cuál es natural en la vida real). Por contra, los microservicios proponen como solución que cada funcionalidad de un proyecto ha de ser identificada y aislada como un proceso/servicio independiente, atendiendo al principio de única responsabilidad (*single-responsibility principle*). Esto ayuda de antemano a desacoplar las diferentes unidades de un proyecto, lo que a su vez es más beneficioso a la hora de renovar, refactorizar o reinventar partes del mismo, sin tener que atender a más preocupación que la interfaz programática de comunicación (API).

| Ventajas                                                     | Inconvenientes                                        |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| Incrementa la eficiencia: divide la funcionalidad, mejora la escalabilidad | Latencia de red                                       |
| Facilita las actualizaciones                                 | Complejidad del diseño                                |
| Mejora la estabilidad                                        | ¿Qué es un microservicio? Tamaño, funcionalidad, etc. |
| Desacoplado de recursos físicos                              | Estandarización de interfaces                         |
| Multi-idioma/plataforma/…                                    |                                                       |
| Fácil de construir/probar/desplegar                          |                                                       |

 A continuación se muestra una figura en la que se comparan de manera esquemática las arquitecturas tradicionales *versus* las arquitecturas orientadas a microservicios.![soa-vs-microservices](/Users/mduranol/Dropbox/Root/Home/Documents/ICAI/course-2021/teaching/ASR/theory/images/soa-vs-microservices.png)



#### Orquestación de contenedores: Kubernetes

Si prestamos suficiente atención a nuestro QuickLab (QL) I veremos que lo que realmente hemos hecho es preparar dos microservicios (cada uno con una responsabilidad única y bien definida, ver [*Single Responsibility Principle*](https://en.wikipedia.org/wiki/Single-responsibility_principle)) que posteriormente hemos desplegado en GCP. Cuando llegamos a este punto en el capítulo de virtualización vimos que ***en local*** podíamos "orquestar" (gestionar de manera conjunta y organizada un conjunto de) contenedores mediante el uso de [Docker Compose](https://docs.docker.com/compose/). Para ello se usaba **docker compose engine**, un comando de terminal que en última instancia dependía de un fichero (manifiesto) de configuración que se solía llamar `docker-compose.yaml` donde especificábamos los contenedores a crear/lanzar, sus configuraciones de red/puertos, además de su volúmenes etc. Un ejemplo sencillo era:

```yaml
version: "3.9"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"	
```

Que posteriormente usábamos mediante:

```shell
$ docker-compose up
```

lo cual ponía en marcha una API (que se especificaba en el Dockerfile que construíamos como `web`) que permitía insertar registros en una base de datos [`redis`](https://redis.io/), y que posteriormente podíamos parar con una simple línea de comandos:

```bash
$ docker-compose stop
```

Inmediatamente vimos la conveniencia y eficiencia que `docker-compose` traía a nuestro ecosistema de desarrollo. Pero, también vimos una *pequeña* inconveniencia, que de hecho no es tan pequeña en el caso que nuestro objetivos se el disponer de una arquitectura flexible, dinámica y fácilmente gestionable. Con `docker-compose`  gestionamos contenedores, pero todos los servicios conviven en el mismo host. La pregunta natural entonces es, ¿Cómo podríamos hacer que cada contenedor sea desplegado en un host distinto y de forma que pueda ser autoescalado independiente? 

Para este problema de orquestación de contenedores y arquitectura asociada existen principalmente dos soluciones: `docker swarm` y `kubernetes engine`. Aunque ambos dos proponen una solución a un mismo problema, existen pequeñas diferencias que hacen que Kubernetes haya sido el más usado en la industria. Muy resumidamente:

- [Docker swarm](https://docs.docker.com/engine/swarm/): es una herramienta de orquestación de contenedores, la cual nos permite llegar a la solución deseada de lanzar imágenes en diferentes máquinas (hosts) 
- [Kubernetes](https://kubernetes.io/): es una herramienta de orquestación de contenedores, que como en el caso de docker swarm nos permite el lanzamiento de imágenes en diferentes hosts, pero su *focus* principal ha sido la automatización y habilidad de adaptarse a escenarios de alta demanda 

Así pues, se puede decir que la mayor diferencia entre Docker swarm y Kubernetes es la facilidad de uso. Nada ilustra mejor esto que un ejemplo sobre cómo cada uno maneja las redes. Cuando se crea un clúster de contenedores con Docker swarm, esos contenedores generalmente están disponibles en nuestra red porque ha dirigido un puerto externo a un puerto interno desde el comando `docker`. En otras palabras, no tenemos que configurar una capa de red separada dentro de los archivos YAML. Sin embargo, con Kubernetes, debemos configurar una capa de red (utilizando declaraciones como `hostNetwork: true` dentro del manifiesto correspondiente). Si no agregamos esta capa de red accesible a la `LAN` dentro de los archivos YAML, no podremos acceder a los contenedores desde cualquier lugar que no sea el clúster de Kubernetes. A pesar que puede parecer que esto añade trabajo a la persona encargada, la realidad es que esto también trae con ello un incremento grandísimo de la reproducibilidad del comportamiento, lo que nos puede salvar bastantes horas de debugging.

Así pues, Docker Swarm es mucho más sencillo en términos de uso y exploración, pero Kubernetes es mucho más escalable. Entonces, ¿cuando deberíamos usar uno u otro?

* **Docker Swarm**: Cuando queremos implementar un cluster de contenedores (en varios hosts) para una aplicación simple y escalable
* **Kubernetes**: Cuando queremos administrar una aplicación de microservicios contenerizados, escalables y automatizados.

Es por esto mismo por lo que los principales proveedores de cloud ofertan directamente Kubernetes. En el caso de Google, Kubernetes se oferta parte de los servicios que podemos usar en la modalidad "pay as you go" y se denomina [**Google Kubernetes Engine**](https://cloud.google.com/kubernetes-engine/docs/quickstart) (GKE).

K8s conlleva una curva de aprendizaje, no cabe ninguna duda. Y por ello, no pretendemos dar un (mini-)curso, sino algunos conceptos básicos y necesarios para introducir esta herramienta de increíble alcance de la que se podría dar un curso completo para su total entendimiento. Finalmente veremos, como viene siendo costumbre, un ejemplo práctico con nuestro QL III.

Conceptos necesarios para entender k8s:

* **Cluster**: Cuando "desplegamos" con k8s, lo que estamos creando/obteniendo es un cluster. Un cluster no es más que un conjunto de VMs (nodos) que ejecutan aplicaciones contenerizadas. Todo cluster tiene al menos un nodo.

* **Node**: Como hemos comentado, un nodo es una instancia de una VM donde se sirven los contenedores de nuestras aplicaciones
* **Pod**: Un pod es una abstracción de k8s que representa un conjunto de contenedores que son servidos en un nodo
* **Control plane**: Se refiere a la capa de orquestación que expone la API e interfaces para definir, desplegar, y gestionar el ciclo de vida de los contenedores. En un entorno productivo, el **control plane** suele estar corriendo en varios nodos, lo que garantiza el servicio en caso de fallos.

Como resumen visual:

<img src="https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg" alt="Components of Kubernetes" style="zoom:80%;" />

Para un entendimiento más profundo de los componentes del **control plane**, ver la [documentación oficial](https://kubernetes.io/es/docs/concepts/overview/components/).

#### Kubernetes gestionado: Google App Engine (GAE)

Una vez hayamos experimentado un poco con K8s (e.g. haciendo los QLs III y IV) será cuestión de tiempo que lleguemos a la pregunta: ¿Cómo podría deshacerme de tanta gestión (programática) y centrarme en el desarrollo en el caso que mi objetivo central sea el producto? Si revisamos el material que hemos estudiado hasta ahora, la respuesta a tal pregunta tiene una realidad conocida como **PaaS**. En el contexto de GCP, el servicio que nos permite abstraernos de la gestión de la infraestructura y centrarnos en el desarrollo de Apps es conocido como [Google App Engine](https://cloud.google.com/appengine/docs/standard/python3/an-overview-of-app-engine) (GAE).

GAE nos brinda la oportunidad de las bondades de K8s, tales como el autoescalado, sin que tengamos que ser nosotros los que nos preocupemos por gestionar el cluster. Así, GAE se puede entender como un cluster de K8s gestionado automáticamente por Google. Es por ello por lo que todos nuestros esfuerzos se pueden centrar única y exclusivamente en el desarrollo del software (app), dejando la gestión del cluster a Google (sin más que especificar algunas propiedades del cluster para controlar costes, como pueden ser el máximo numero de instancias, etc.)

Podemos entender GAE como el servicio ideal donde desplegar nuestros micro-servicios, los cuales conjuntamente constituyen un ecosistema interconectado, sobre el que podremos ir construyendo capas superiores de abstracción con el fin de acabar con el desarrollo monolítico. 

Una vez tengamos una versión inicial de nuestro aplicativo (app), podremos servirlo inmediatamente en uno de los dos entornos proporcionados por GAE:

* **Standard**: En caso que nuestro aplicativo esté escrito en uno de los siguientes lenguajes y versiones:

  * Python 2.7, Python 3.7, Python 3.8, Python 3.9
  * Java 8, Java 11
  * Node.js 10, Node.js 12, Node.js 14, Node.js 16 (preview)
  * PHP 5.5, PHP 7.2, PHP 7.3, and PHP 7.4
  * Ruby 2.5, Ruby 2.6, and Ruby 2.7
  * Go 1.11, Go 1.12, Go 1.13, Go 1.14, Go 1.15, and Go 1.16 (preview)

  Podremos disfrutar de un entorno "standard", de manera que GAE se encargará de contenerizar nuestro código y desplegarlo en instancias a muy bajo coste. 

* **Flexible**: En el caso que nuestro aplicativo esté contenerizado, y queramos lanzarlo como contenedor porque depende de librerías no estándares, o está escrito en un lenguaje no listado, o tiene unas necesidades computacionales algo más exigentes que las ofertadas en el entorno standard. El entorno de despliegue flexible nos permite una mayor personalización en términos de recursos, lo cual puede ser muy conveniente.

Para un mayor entendimiento de la diferencia entre ambos modelos, podemos ver la [documentación oficial](https://cloud.google.com/appengine/docs/the-appengine-environments).

#### Aplicaciones Serverless: El espíritu cloud native

Finalmente, incluso deshaciéndonos de la responsabilidad de mantener el cluster de K8s mediante el uso de GAE, tenemos una limitación y es que seguimos teniendo que mantener un mínimo de 1 instancia (nodo) funcionando 24/7. Sin embargo, nuestro objetivo último siempre ha sido el llegar a una arquitectura que sea lo más dinámica posible, con la idea en mente de escalar hasta cero instancias si fuera posible, de manera que solo pagásemos realmente por aquello que usamos. Y este es precisamente el objetivo de las dos últimos servicios de hosting de aplicativos que vamos a ver, que son:

* Cloud Functions
* Cloud Run

Ambos dos se centran en el concepto de escalar a cero, es decir, de deshacernos del concepto de "servidor" (*serverless*) mediante la gestión activa y automática de infraestructura y plataforma de Google. Como veremos ambos están íntimamente relacionados entre sí, y su diferencia tiene que ver con los environments standard y flexible de GAE.

Este paradigma de desarrollo se conoce como **Funtions as a Service** (FaaS), dado que el objetivo principal es la programación de una funcionalidad (que en última instancia se entiende que se ejecutará en reacción a un evento dado). El esquema IaaS, PaaS y SaaS que vimos anteriormente queda ampliado del siguiente modo:

<img src="https://miro.medium.com/max/1145/1*DYoadhgfpZCMRCMKNUpQ6A.png" alt="What are Cloud Computing Services [IaaS, CaaS, PaaS, FaaS, SaaS] | by  Nilesh Suryavanshi | Medium" style="zoom:67%;" />

De modo que en una arquitectura FaaS (serverless) lo único de lo que tenemos que hacernos cargo es de la gestión de los datos procesados o generados por la "función".

Las ventajas principales son:

* No tendrás que aprovisionar, administrar ni actualizar servidores
* Escala automáticamente según la carga. Se paga por el tiempo de procesamiento de la función
* Funciones integradas de supervisión, registro y depuración 
* Seguridad integrada a nivel de funciones y por función que se basa en el principio de privilegio mínimo
* Capacidades de red clave para situaciones híbridas y de múltiples nubes

##### Functions as a Service (FaaS): Google Cloud Functions

Cloud functions nos brinda la oportunidad única de ir directamente de código a aplicativo serverless sin necesidad de contenerización.

**Serverless Apps**: **Google Cloud Run**

Cloud run se puede entender como el paso intermedio entre GCF y GAE, i.e., con GCR podremos montar un aplicativo serverless cuando nuestro aplicativo ya esté contenerizado.

#### Los 12 factores

“Twelve-factor app” es una metodología para el desarrollo de aplicaciones nativas en la nube cuyas características esenciales son: 

- Formatos declarativos para la automatización de la configuración
- Máxima portabilidad entre los diferentes entornos de ejecución
- Despliegue en la nube, por lo que se obviará la necesidad de servidores y administración de sistemas
- Minimizan las diferencias entre los entornos de desarrollo y producción
- Posibilidad de escalado

Los 12 factores son: 

1. **Codebase**: Un código base sobre el que hacer el control de versiones y múltiples despliegues. 
2. **Dependencies**: Declarar y aislar explícitamente las dependencias mediante un manifiesto. Nunca dependerá de las librerías ya instaladas en el sistema por defecto
3. **Config**: Guardar la configuración en el entorno que pueda variar entre despliegues (producción o desarrollo, por ejemplo)
4. **Backing services**: Tratar a los “backing services” como recursos conectables
5. **Build, release, run**: Separar completamente la etapa de construcción de la etapa de ejecución
6. **Processes**: Ejecutar la aplicación como uno o más procesos sin estado. Los procesos deben ser stateless y share-nothing. Cualquier información que necesite persistencia se debe almacenar en un backing service con estado (e.g., una base de datos). 
7. **Port binding**: En entornos locales un servicio como un servidor web inicia en un puerto para todas las apps. En 12-factor apps, una capa de enrutamiento se encargará de gestionar los puertos de cada servicio
8. **Concurrency**: Escalar mediante el modelo de procesos
9. **Disposability**: Hacer el sistema más robusto intentando conseguir inicios rápidos y finalizaciones seguras. Las 12- factor apps deberán ser plenamente desechables en cualquier momento. 
10. **Dev/prod parity**: Mantener desarrollo, preproducción y producción tan parecidos como sea posible 
11. **Logs**: Tratar los historiales como una transmisión de eventos. 
12. **Admin processes**: Ejecutar las tareas de gestión/administración como procesos que solo se ejecutan una vez. 

“[Twelvefactor](https://12factor.net/)” recomienda lenguajes que proporcionan una consola del tipo REPL, ya que facilitan las tareas relacionadas con la ejecución de scripts

#### QuickLabs

Para reforzar los conceptos que vamos introduciendo de manera teórica hemos diseñado varios ejemplos en los que iremos trabajando con la nube de Google (GCP). En este momento, tras haber introducido las ventajas e inconvenientes de la contenerización y los microservicios, es interesante que procedamos con los siguientes ejemplos:

##### 💻 QuickLab I: Creación y despliegue de contenedores en GCP

* Creación y despliegue de un microservicio con Flask que nos permite la inserción y borrado de registros mediante una API sencilla en una base de datos *in-memory* (redis). El objetivo de este ejemplo es el de mostrar la estructura típica de una aplicación con varios microservicios, y la gestión de su despliegue de manera programática (pero aún manual) en la nube mediate Google SDK. El código y sumario de este QuickLab pueden encontrarse en este [link]( https://github.com/**PENDING**/asr-cloud/tree/main/03-flask-redis).   

##### 💻 QuickLab II: SuperMario auto-escalable

* Creación y despliegue de una aplicación dada (como Docker Image) con autoescalado y balanceado de carga. El objetivo es ir un paso más allá del ejemplo anterior, y mostrar lo conveniente que es la contenerización de aplicaciones para su despliegue en una infraestructura autoescalable según la utilización del servicio. Para ello tendremos que crear un grupo de instancias gestionadas que se desplieguen con la imagen de la aplicación en el arranque, y que autoescalen a medida que sea necesario acorde a un umbral de utilización. Para servir la aplicación con una única IP a nuestros poténciales clientes, tendremos que crear un balanceado de carga (con *Cloud Load Balancer*) que hará la el enrutamiento correcto a la VM adecuada. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/04-autoscaling-mario). 

##### 💻 QuickLab III: SuperMario con K8s

* El objetivo es ir un paso más allá del ejemplo anterior, y mostrar lo conveniente que es la utilización de GKE. Para ello tendremos que crear un cluster de K8s en GCP. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/05-k8s-init). 

##### 💻 QuickLab IV: Soluciones y estrategias de autoescalado con K8s

* Este lab es uno de los más técnicos que vamos a tener, precisamente para entender la complejidad de K8s, además de la infinidad de configuraciones posibles existentes (a pesar de tan solo explorar una pequeñísima fracción del todo en este ejemplo). En particular, veremos la posibilidad de escalar horizontal y verticalmente a nivel POD, para posteriormente ver cómo este escalamiento horizontal y vertical se puede realizar a nivel cluster. Este nivel de control de un cluster es necesario cuando trabajemos con proyectos productivos, en los que queremos una máxima estabilidad y resiliencia del servicio, pero al menor coste posible (es decir, con la menor cantidad de infraestructura), y a su vez que la infraestructura se adapte automáticamente a los picos de demanda tan característicos del entorno digital de hoy en día. Como se puede desprender del enunciado del objetivo del lab, el problema es algo bastante complicado. El hecho que GKE nos permita esta gestión de manera automática y nos provea con soluciones para gestionar este automatismo es lo que hace que GKE sea el número uno en la gestión de contenedores en entornos cloud. Sin embargo, también vamos a ver con ello el intenso trabajo que esta configuración, mantenimiento y monitorización requiere. Es por ello por lo que el siguiente paso natural es intentar evitar susodicha gestión a menos que sea absolutamente necesaria. Pensando en ello, todos los proveedores cloud a día de hoy proporcionan soluciones de K8s gestionados. En el caso de Google se tratará de Google App Engine (con el que trabajaremos en el siguiente QL). El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](**PENDING**). 

💻 **QuickLab V: App Engine**

* En este lab el objetivo es demostrar la sencillez del despliegue y mantenimiento de una App que se despliega en [Google App Engine](https://cloud.google.com/appengine/docs) (GAE). Para ello, vamos a desplegar un Super Mario auto-escalable, con un simple comando, y sin necesidad de tener que gestionar nosotros el tipo de escalado. GAE nos ofrece automáticamente la posibilidad de un auto-escalado (horizontal) automático, además de una gestión del balanceamiento de carga automático. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/07-gae-example).

💻 **QuickLab VI: Cloud Functions**

* El objetivo de este lab es la demostración de como podemos desplegar de manera sencilla una función en Google Cloud Function. Para este propósito hemos creado una función en Python cuyo "trigger" es una llamada HTTP. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/08-cloud-functions).

💻 **QuickLab VI: Cloud Run**

* Tal y como hemos comentado en clase, existe una segunda opción para desplegar apps serverless, que tiene la conveniencia de aceptar **Docker Images** en lugar de **Functions**. Esta opción en GCP se llama Google Cloud Run. En este lab ponemos de manifiesto la sencillez y conveniencia del uso de GCR (documentación oficial [aquí](https://cloud.google.com/run)). El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/09-cloudrun). En este lab se muestran también opciones de gestión programática y de CICD.

