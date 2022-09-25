### Kubernetes gestionado: Google App Engine (GAE)

GAE nos brinda la oportunidad de las bondades de K8s, tales como el autoescalado, sin que tengamos que ser nosotros los que nos preocupemos por gestionar el cluster. Así, GAE se puede entender como un cluster de K8s gestionado automáticamente por Google. Es por ello por lo que todos nuestros esfuerzos se pueden centrar única y exclusivamente en el desarrollo del software (app), dejando la gestión del cluster a Google (sin más que especificar algunas propiedades del cluster para controlar costes, como pueden ser el máximo numero de instancias, etc.)

Podemos entender GAE como el servicio ideal donde desplegar nuestros micro-servicios, los cuales conjuntamente constituyen un ecosistema interconectado, sobre el que podremos ir construyendo capas superiores de abstracción con el fin de acabar con el desarrollo monolítico. 

Una vez tengamos una versión inicial de nuestro aplicativo (app), podremos servirlo inmediatamente en uno de los dos entornos proporcionados por GAE:

* **Standard**: En caso que nuestro aplicativo esté escrito en uno de los siguientes lenguajes y versiones:

  * Python, Java, Node.js, PHP, Ruby, GO

  Podremos disfrutar de un entorno "standard", de manera que GAE se encargará de contenerizar nuestro código y desplegarlo en instancias a muy bajo coste. 

* **Flexible**: En el caso que nuestro aplicativo esté contenerizado, y queramos lanzarlo como contenedor porque depende de librerías no estándares, o está escrito en un lenguaje no listado, o tiene unas necesidades computacionales algo más exigentes que las ofertadas en el entorno standard. El entorno de despliegue flexible nos permite una mayor personalización en términos de recursos, lo cual puede ser muy conveniente.

Para un mayor entendimiento de la diferencia entre ambos modelos, podemos ver la [documentación oficial](https://cloud.google.com/appengine/docs/the-appengine-environments).


### Aplicaciones Serverless: El espíritu cloud native

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

### Functions as a Service (FaaS): Google Cloud Functions

Cloud functions nos brinda la oportunidad única de ir directamente de código a aplicativo serverless sin necesidad de contenerización.

**Serverless Apps**: **Google Cloud Run**


##### 💻 QuickLab V: Soluciones y estrategias de autoescalado con K8s

* Este lab es uno de los más técnicos que vamos a tener, precisamente para entender la complejidad de K8s, además de la infinidad de configuraciones posibles existentes (a pesar de tan solo explorar una pequeñísima fracción del todo en este ejemplo). En particular, veremos la posibilidad de escalar horizontal y verticalmente a nivel POD, para posteriormente ver cómo este escalamiento horizontal y vertical se puede realizar a nivel cluster. Este nivel de control de un cluster es necesario cuando trabajemos con proyectos productivos, en los que queremos una máxima estabilidad y resiliencia del servicio, pero al menor coste posible (es decir, con la menor cantidad de infraestructura), y a su vez que la infraestructura se adapte automáticamente a los picos de demanda tan característicos del entorno digital de hoy en día. Como se puede desprender del enunciado del objetivo del lab, el problema es algo bastante complicado. El hecho que GKE nos permita esta gestión de manera automática y nos provea con soluciones para gestionar este automatismo es lo que hace que GKE sea el número uno en la gestión de contenedores en entornos cloud. Sin embargo, también vamos a ver con ello el intenso trabajo que esta configuración, mantenimiento y monitorización requiere. Es por ello por lo que el siguiente paso natural es intentar evitar susodicha gestión a menos que sea absolutamente necesaria. Pensando en ello, todos los proveedores cloud a día de hoy proporcionan soluciones de K8s gestionados. En el caso de Google se tratará de Google App Engine (con el que trabajaremos en el siguiente QL). El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](**PENDING**). 

💻 **QuickLab VI: Cloud Run**

* Tal y como hemos comentado en clase, existe una segunda opción para desplegar apps serverless, que tiene la conveniencia de aceptar **Docker Images** en lugar de **Functions**. Esta opción en GCP se llama Google Cloud Run. En este lab ponemos de manifiesto la sencillez y conveniencia del uso de GCR (documentación oficial [aquí](https://cloud.google.com/run)). El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/09-cloudrun). En este lab se muestran también opciones de gestión programática y de CICD.



💻 **QuickLab VI: Cloud Functions**

* El objetivo de este lab es la demostración de como podemos desplegar de manera sencilla una función en Google Cloud Function. Para este propósito hemos creado una función en Python cuyo "trigger" es una llamada HTTP. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/08-cloud-functions).


