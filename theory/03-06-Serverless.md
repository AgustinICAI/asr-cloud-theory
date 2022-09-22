
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


💻 **QuickLab VI: Cloud Functions**

* El objetivo de este lab es la demostración de como podemos desplegar de manera sencilla una función en Google Cloud Function. Para este propósito hemos creado una función en Python cuyo "trigger" es una llamada HTTP. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/08-cloud-functions).

💻 **QuickLab VI: Cloud Run**

* Tal y como hemos comentado en clase, existe una segunda opción para desplegar apps serverless, que tiene la conveniencia de aceptar **Docker Images** en lugar de **Functions**. Esta opción en GCP se llama Google Cloud Run. En este lab ponemos de manifiesto la sencillez y conveniencia del uso de GCR (documentación oficial [aquí](https://cloud.google.com/run)). El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**/asr-cloud/tree/main/09-cloudrun). En este lab se muestran también opciones de gestión programática y de CICD.


