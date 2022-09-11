# 3. Cloud Computing

### 3.6 Gestión programática del Cloud

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

* El objetivo de este Lab es el de presentar las posibilidades ofrecidas por [Google Cloud Deployment Manager](https://cloud.google.com/deployment-manager/). En particular, vamos a crear un manifiesto de configuración que enuncia la creación de dos máquinas virtuales. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/migduroli/asr-cloud/tree/main/11-deployment-manager).

💻 **QuickLab VIII: Terraform**

* El objetivo de este Lab es el de presentar las posibilidades ofrecidas por [Terraform](https://www.terraform.io/). En particular, vamos a crear un fichero de configuración que enuncia la creación de una máquina virtual. El código y sumario de este QuickLab se puede encontrar en el siguiente: [link](https://github.com/migduroli/asr-cloud/tree/main/12-terraform).
