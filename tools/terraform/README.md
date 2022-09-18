# 3. Cloud Computing

### 3.6 Gestión programática del Cloud

##### Terraform

Como hemos comentado, Terraform es una herramienta alternativa que ha ganado mucha tracción en los últimos años en el ámbito de la gestión de infraestructura como código versionado. Una ventaja indiscutible de Terraform es que nos brinda la posibilidad de tratar con un lenguaje unificado las diferentes infraestructuras que podemos tener en distintas nubes públicas (y privadas), e.g. en Google Cloud, Microsoft Azure y AWS.

Todo lo que necesitamos para la gestión de infraestructura con Terraform es la codificación de la misma en un manifiesto de configuración. Dicho fichero de configuración describirá los diferentes componentes que necesitamos asociar a una aplicación. Además, Terraform no solo es capaz de trabajar con componentes de bajo nivel como pueden ser instancias de VMs, almacenamiento of redes, sino que también trabaja con el despliegue y gestión de componentes de más alto nivel como DNS y servicios SaaS ofertados por los proveedores.

Las principales características de Terraform son las siguientes:

###### Infraestructura como código (IaC)

Como ya hemos comentado, la infraestructura se describe como código usando una sintaxis de muy alto nivel. Esto permite el versionado de toda la infraestructura de nuestro proyecto, al igual que haríamos con cualquier aplicativo. 

###### Planes de ejecución

Terraform tiene una etapa de planificación en la cual se genera un plan de ejecución. Este plan nos mostrará los diferentes pasos que Terraform seguirá cuando finalmente apliquemos (`apply`) nuestro manifiesto de configuración. Esta característica es muy importante a la hora de evitar sorpresas antes de la ejecución.

###### Grafos de recursos

Terraform generará un grafo de todos los recursos y paraleliza la creación y modificación de cualquier componente que no esté interconectado con otro. El objetivo de ello es la generación y mantenimiento de infraestructura en la forma más eficiente posible. Así, como colateral, los Operadores de nuestra infraestructura tendrán conocimiento en todo momento de la interconexión de los elementos de la misma, lo que nos puede servir para planificar futuras mejoras desde muy temprano.

###### Automatización de cambios

Terraform nos permite la aplicación de cambios complejos a nuestra infraestructura con una mínima interacción humana. Con los planes de ejecución y los grafos de recursos, sabemos exactamente qué es lo que se va a cambiar en cada despliegue y en qué orden, de manera que se minimizan errores humanos debidos a las complejas interdependencias que pueden existir en un proyecto.

Para un conocimiento más detallado de Terraform, sugerimos acudir a la documentación oficial [aquí](https://www.terraform.io/).




