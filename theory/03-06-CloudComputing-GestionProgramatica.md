# 3. Cloud Computing

### 3.6 Gestión programática del Cloud

Hasta ahora hemos estado trabajando con las herramientas de gestión nativas de la nube de Google Cloud. Para ello, como ha sido costumbre en todos y cada uno de los QLs, hemos usado `gcloud` para la creación y destrucción de recursos, desde `buckets` en Google Cloud Storage, hasta `compute instances`, `firewall rules` o incluso `datasets` y `tables` en Google **BigQuery**. Y esto son muy buenas noticias, porque casi sin darnos cuenta, ya hemos estado haciendo una gestión programática de la nube!

No obstante, a pesar de lo útil que nos ha sido hasta ahora, las soluciones que hemos creado hasta ahora con la conveniencia del uso inmediato de Google SDK no son escalables, dado que han estado muy ligadas a nuestros casos de estudio particulares. Además, cada uno de susodichos scripts viven por separado y no hay (como admin) una forma sencilla de tener una visión general de todos los despliegues existentes siguiendo este método. Por ejemplo, ¿qué ocurriría si en lugar de tener un despliegue diario a GKE tuviéramos cientos o incluso miles de ellos, como puede ser el caso de una compañía tecnológica?. En tal caso, tendríamos que gestionar con scripts manuales cientos de procesos de despliegue en diferentes entornos de desarrollo, y esto evidentemente sería seguramente imposible. No obstante, existen herramientas que nos harán mucho más sencilla la gestión de nuestra infraestructura de una forma programática cumpliendo los 12 factores, y por tanto convirtiendo nuestra infraestructura en código "cloud native". En el mundo GCP tenemos dos opciones:

* Google Cloud [Deployment Manager](https://cloud.google.com/deployment-manager): Es la solución propuesta por Google para la gestión de infraestructura con código, automatizando la creación y la gestión de los recursos cloud. Dicha gestión 
* [Terraform](https://www.terraform.io/): Es una herramienta *open source* para la gestión de infraestructura con código que nos proporciona una línea de comandos independiente del proveedor de nube. 

Aunque vamos a ver un ejemplo de cada uno de estas posibilidades, es cierto que para evitar la dependencia exclusiva del proveedor de Google, muchas empresas han optado por gestionar sus nubes con Terraform, por su independencia y por la posibilidad de abstraernos del proveedor, con las ventajas que ello conlleva en el futuro si tuviéramos que migrar de una nube a otra por ejemplo.

##### Deployment manager

Antes de proceder a un ejemplo, tenemos que asegurarnos que tenemos activada las siguientes APIs en nuestro proyecto:

* Compute Engine API
* Cloud Deploy API

El primer paso para tener un *pipeline* de despliegue y gestión de infraestructura con Cloud Deploy es codificar nuestro manifiesto de configuración, que será tipo YAML. En este archivo de configuración es donde especificaremos todas las variables de configuración de los diferentes recursos de infraestructura que queremos crear. Esto será siempre especificado en una sección del fichero YAML  que se denominará `resources`. Colgando de dicha sección, tendremos tantas sub-secciones como recursos queramos reservar, listados con un guión, y siempre comenzando con su nombre, campo `name`. Un ejemplo básico de un prototipo de YAML sería:

```yaml
resources:
- name: the-first-vm
  type: compute.v1.instance
  properties:
  	...
- name: the-second-vm
  type: compute.v1.instance
  properties:
		...
```

Donde, por ejemplo, estaríamos indicando la creación de dos VMs, cuyas propiedades específicas hemos dejado para el QL correspondiente.

Ahora que ya tenemos una configuración de despliegue, ya podemos crear el susodicho despliegue. Para ello vamos a usar:

```shell
$ gcloud deployment-manager deployments create DEPLOYMENT_NAME \
		--config CONFIGURATION_FILE_NAME.yaml
```

Lo que creará un *deployment* con nombre `DEPLOYMENT_NAME` a partir del fichero `CONFIGURATION_FILE.yaml`.

Aunque a primera vista puede parecer que lo realizado es idéntico a lo ya estudiado y hecho con el uso directo de `gcloud` para cada uno de los recursos, Cloud Deploy permite la creación de templates de despliegues re-utilizables para otros despliegues, eliminando por tanto la especificidad de los scripts ad-hoc. Además, Cloud Deploy es auditable, además de brindarnos la comodidad de tener un portal de monitorización de despliegues. Por ejemplo, tras el despliegue del manifiesto con dos VMs, tendremos en nuestro portal web algo como la siguiente imagen:

 <img src="/Users/mduranol/Dropbox/Root/Home/Documents/ICAI/course-2021/teaching/ASR/theory/images/deployment-manager.png" alt="deployment-manager" style="zoom:67%;" />

Para un conocimiento más profundo de las múltiples opciones de Deployment Manager, podemos acudir a la documentación oficial aquí.

##### Terraform

Como hemos comentado, Terraform es una herramienta alternativa que ha ganado mucha tracción en los últimos años en el ámbito de la gestión de infraestructura como código versionado. Una ventaja indiscutible de Terraform es que nos brinda la posibilidad de tratar con un lenguaje unificado las diferentes infraestructuras que podemos tener en distintas nubes públicas (y privadas), e.g. en Google Cloud, Microsoft Azure y AWS.

Al igual que en el caso de Deployment Manager, todo lo que necesitamos para la gestión de infraestructura con Terraform es la codificación de la misma en un manifiesto de configuración. Dicho fichero de configuración describirá los diferentes componentes que necesitamos asociar a una aplicación. Además, Terraform no solo es capaz de trabajar con componentes de bajo nivel como pueden ser instancias de VMs, almacenamiento of redes, sino que también trabaja con el despliegue y gestión de componentes de más alto nivel como DNS y servicios SaaS ofertados por los proveedores (una ventaja en comparación con Deployment Manager).

Las principales características de Terraform son las siguientes:

###### Infraestructura como código (IaaS)

Como ya hemos comentado, la infraestructura se describe como código usando una sintaxis de muy alto nivel. Esto permite el versionado de toda la infraestructura de nuestro proyecto, al igual que haríamos con cualquier aplicativo. 

###### Planes de ejecución

Terraform tiene una etapa de planificación en la cual se genera un plan de ejecución. Este plan nos mostrará los diferentes pasos que Terraform seguirá cuando finalmente apliquemos (`apply`) nuestro manifiesto de configuración. Esta característica es muy importante a la hora de evitar sorpresas antes de la ejecución.

###### Grafos de recursos

Terraform generará un grafo de todos los recursos y paraleliza la creación y modificación de cualquier componente que no esté interconectado con otro. El objetivo de ello es la generación y mantenimiento de infraestructura en la forma más eficiente posible. Así, como colateral, los Operadores de nuestra infraestructura tendrán conocimiento en todo momento de la interconexión de los elementos de la misma, lo que nos puede servir para planificar futuras mejoras desde muy temprano.

###### Automatización de cambios

Terraform nos permite la aplicación de cambios complejos a nuestra infraestructura con una mínima interacción humana. Con los planes de ejecución y los grafos de recursos, sabemos exactamente qué es lo que se va a cambiar en cada despliegue y en qué orden, de manera que se minimizan errores humanos debidos a las complejas interdependencias que pueden existir en un proyecto.

Para un conocimiento más detallado de Terraform, sugerimos acudir a la documentación oficial [aquí](https://www.terraform.io/).

###### Tres sencillos pasos

Por último, toda la gestión (una vez programado el fichero de configuración) se hará ejecutando los siguientes tres (dos después de la primera inicialización) pasos:

1. `terraform init`: En este paso se descargará un plugin del proveedor cloud (Google en nuestro caso), y se guardará en un subdirectorio del directorio en el que nos encontremos trabajando. 
2. `terraform plan`: En este paso Terraform realiza un estudio sobre las acciones que serán necesarias dado el fichero de configuración con el que estamos trabajando. Susodicho plan será impreso por pantalla, pero podremos guardarlo en un fichero a nuestro antojo con la opción `-o`. 
3. `terraform apply`: Tras una planificación, solo falta la aplicación de la misma, y es con este comando con el que finalmente se ejecutarán los pasos anteriormente planificados. 

Un ejemplo del resultado de estas acciones sería:

```
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create
Terraform will perform the following actions:
  # google_compute_instance.default will be created
  + resource "google_compute_instance" "default" {
      + can_ip_forward       = false
      + cpu_platform         = (known after apply)
      + deletion_protection  = false
      + guest_accelerator    = (known after apply)
      + id                   = (known after apply)
      + instance_id          = (known after apply)
      + label_fingerprint    = (known after apply)
      + machine_type         = "n1-standard-1"
      + metadata_fingerprint = (known after apply)
      + name                 = "terraform"
      + project              = "qwiklabs-gcp-42390cc9da8a4c4b"
      + self_link            = (known after apply)
      + tags_fingerprint     = (known after apply)
      + zone                 = "us-central1-a"
      + boot_disk {
          + auto_delete                = true
          + device_name                = (known after apply)
          + disk_encryption_key_sha256 = (known after apply)
          + kms_key_self_link          = (known after apply)
          + source                     = (known after apply)
          + initialize_params {
              + image  = "debian-cloud/debian-9"
              + labels = (known after apply)
              + size   = (known after apply)
              + type   = (known after apply)
            }
        }
      + network_interface {
          + address            = (known after apply)
          + name               = (known after apply)
          + network            = "default"
          + network_ip         = (known after apply)
          + subnetwork         = (known after apply)
          + subnetwork_project = (known after apply)
          + access_config {
              + assigned_nat_ip = (known after apply)
              + nat_ip          = (known after apply)
              + network_tier    = (known after apply)
            }
        }
      + scheduling {
          + automatic_restart   = (known after apply)
          + on_host_maintenance = (known after apply)
          + preemptible         = (known after apply)
          + node_affinities {
              + key      = (known after apply)
              + operator = (known after apply)
              + values   = (known after apply)
            }
        }
    }
Plan: 1 to add, 0 to change, 0 to destroy.
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.
  Enter a value:
```

Si el plan se ha generado correctamente, Terraform se esperará a la confirmación y aprobación por parte del administrador para proceder a su ejecución. De esta forma, si estamos en un entorno productivo y vemos algo **peligroso** en la planificación, podemos parar sin ninguna consecuencia.

Para ver Terraform en acción ir al QL correspondiente de ésta sección. 

💻 **QuickLab VII: Deployment Manager**

* El objetivo de este Lab es el de presentar las posibilidades ofrecidas por [Google Cloud Deployment Manager](https://cloud.google.com/deployment-manager/). En particular, vamos a crear un manifiesto de configuración que enuncia la creación de dos máquinas virtuales. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**roli/asr-cloud/tree/main/11-deployment-manager).

💻 **QuickLab VIII: Terraform**

* El objetivo de este Lab es el de presentar las posibilidades ofrecidas por [Terraform](https://www.terraform.io/). En particular, vamos a crear un fichero de configuración que enuncia la creación de una máquina virtual. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/**PENDING**roli/asr-cloud/tree/main/12-terraform).
