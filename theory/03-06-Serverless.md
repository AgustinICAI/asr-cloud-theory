# 3.6 Serverless

El esquema IaaS, PaaS y SaaS que vimos en el capítulo de [plataformas cloud](03-03-CloudComputing-Plataformas.md)
se puede ampliar con dos modelos adicionales, más orientados a contenedores y funciones:

| | **Infraestructura (IaaS)** | **Plataforma (PaaS)** | **Contenedor (CaaS)** | **Función (FaaS)** | **Software (SaaS)** |
|---|---|---|---|---|---|
| **Ejemplos** | AWS EC2, GCE, Azure VMs | AWS Elastic Beanstalk, App Engine, Azure Web Apps, EKS, GKE, AKS | Fargate, Cloud Run, Azure Container Apps / Container Instances | Lambda, GCF, Azure Functions | Salesforce, Oracle, SAP, Google Workspace, Office 365 |

### Aplicaciones Serverless: El espíritu cloud native

Las [plataformas de desarrollo clásicas](03-03-CloudComputing-Plataformas.md#plataformas-de-desarrollo-en-desuso) (PaaS como App Engine o Elastic Beanstalk) nos liberan de gestionar servidores, pero tienen una limitación: seguimos teniendo que mantener un mínimo de 1 instancia funcionando 24/7. Sin embargo, nuestro objetivo último siempre ha sido el llegar a una arquitectura que sea lo más dinámica posible, con la idea en mente de escalar hasta cero instancias si fuera posible, de manera que solo pagásemos realmente por aquello que usamos. Y este es precisamente el objetivo de las dos últimos servicios de hosting de aplicativos que vamos a ver, que son:

* Cloud Functions
* Cloud Run

Ambos dos se centran en el concepto de escalar a cero, es decir, de deshacernos del concepto de "servidor" (*serverless*) mediante la gestión activa y automática de infraestructura y plataforma de Google. Como veremos ambos están íntimamente relacionados entre sí (de hecho, Google ha integrado Cloud Functions dentro de Cloud Run con el nombre de *Cloud Run functions*), y su diferencia está en qué desplegamos: en Cloud Functions, directamente el código de una función; en Cloud Run, un contenedor.

Este paradigma de desarrollo se conoce como **Functions as a Service** (FaaS), dado que el objetivo principal es la programación de una funcionalidad (que en última instancia se entiende que se ejecutará en reacción a un evento dado).

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

💻 **QuickLab VII-02: Cloud Functions**

* El objetivo de este lab es la demostración de como podemos desplegar de manera sencilla una función en Google Cloud Function. Para este propósito hemos creado una función en Python cuyo "trigger" es una llamada HTTP. El enunciado de esta práctica está en [asr-cloud-26/09-serverless/01-cloud-functions](https://github.com/AgustinICAI/asr-cloud-26/tree/main/09-serverless/01-cloud-functions).


💻 **QuickLab VII-03: Cloud Run**

* Tal y como hemos comentado en clase, existe una segunda opción para desplegar apps serverless, que tiene la conveniencia de aceptar **Docker Images** en lugar de **Functions**. Esta opción en GCP se llama Google Cloud Run. En este lab ponemos de manifiesto la sencillez y conveniencia del uso de GCR (documentación oficial [aquí](https://cloud.google.com/run)). El enunciado de esta práctica está en [asr-cloud-26/09-serverless/02-cloudrun](https://github.com/AgustinICAI/asr-cloud-26/tree/main/09-serverless/02-cloudrun). En este lab se muestran también opciones de gestión programática y de CICD.
