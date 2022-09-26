Ansible es una plataforma para automatización IT para hacer que el proceso de set-up y configuración sistemas sea industriazible a medida que el volumen de infraestructura crece.

# Componentes

## ANSIBLE CLI


### Instalación

```shell
sudo apt-get install ansible
```

### Inventario y primeras automatizaciones

Configurando el inventario de servidores en Ansible
Ansible trabaja con un inventario de servidores. Este inventario se configura por defecto en '/etc/ansible/hosts' y tiene la siguiente forma:
```bash
[desarrollo]
192.168.15.1
192.168.15.2

[preproduccion]
192.168.18.1
192.168.18.2

[produccion]
192.168.20.1
#Si se desea modificar la clave ssh por defecto, se indicaría de la siguiente forma
192.168.20.2 ansible_ssh_private_key_file=~/.ssh/ansible
```

** Para profundizar en como gestionar inventarios con mayor nivel de anidamiento, o incluso inventarios dinámicos integrando con GCP se puede revisar la siguiente documentación:
https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html **


Tal como se ve es un listado de IPs que se agrupan, por ejemplo, aquí el grupo de servidores 'desarrollo' tiene los servidores 192.168.15.1 y 192.168.15.2.

#### Máquinas - Configurando los certificados de seguridad

```shell
ssh-keygen -f ./ansible
```

#### En el caso que trabajemos con un proveedor cloud, por defecto no existirá (ni debe existir) conectividad con la máquina. Es necesario:
1. Obtener acceso directo a la máquina. Puede ser desde un cloud shell o desde tu equipo.
2. En caso de hacerlo desde tu equipo será necesario abrir las reglas firewall que permitan este acceso.
3. Añadir la clave creada en el paso anterior en la consola del proveedor para poder acceder a la máquina. 

En el caso de GCP se haría desde la siguiente pantalla

<img src="images/gcp-ssh-metadata.png" alt="azure-console" style="zoom:67%;" />


Ahora que ya tenemos todo instalado y configurado ya podemos empezar a ejecutar comandos. La sintaxis de Ansible es la siguiente:
```shell
ansible all -m ping
```
```shell
ansible  <servidor/grupo/pattern> -m <módulo> -a <argumentos>
```

De esta manera podemos ejecutar cantidad de cosas:

#### Reiniciar el servicio httpd en los servidores de  preproduccion
```shell
ansible preproduccion -m service -a "name=httpd state=restarted"
```

#### Copiar el fichero 'hola.txt' a los servidores de 'preproduccion' y 'produccion'
```shell
ansible preproduccion:produccion -m copy -a "src=~/prueba/hola.txt dest=/opt/hola.txt"
```

#### Ejecutar '/bin/echo hello' en el servidor '192.168.15.1'. Si no ponemos módulo interpreta que el módulo es 'shell'
```shell
ansible 192.168.15.1 -m shell -a "/bin/echo hello"
ansible 192.168.15.1 -a "/bin/echo hello"
```
Así de fácil es montarte un sistema automatizado con Ansible, tenéis la documentación completa aquí http://docs.ansible.com/ .

## PLAYBOOKS
Se trata de las plantillas que se utilizan para lanzar instrucciones ordenadas sin ningún tipo de interacción humana. Estas plantillas pueden ser tanto para crear infraestructura o/y interactuar con la infraestructura para la instalación/configuración de componentes.

Los módulos de Ansible ejecutan tareas. Se pueden combinar una o más tareas de Ansible para hacer un "play". Se pueden combinar dos o más "plays" para crear un Ansible Playbook. Los Playbooks de Ansible son listas de tareas que se ejecutan automáticamente en los hosts. Los grupos de hosts forman su inventario de Ansible. (como hemos visto con el CLI)

Cada módulo dentro de Ansible Playbook realiza una tarea específica. Cada módulo contiene metadatos que determinan cuándo y dónde se ejecuta una tarea, así como qué usuario la ejecuta, que outputs genera y la concatenación de estas tareas.

Se va a ver más en detalle en la práctica de 4 de IaC, Ansible.

## Ansible Tower / AWX

Ansible Tower (Ansible AWX la versión opensource) es una interfaz de usuario web que permite interaccionar con Ansible para la gestión de inventarios.

Permite a los administradores de sistemas y los equipos de DEVOPS la automatización de tareas contra servidores ofrenciendo los siguientes puntos adicionales:

- Dashboard de usuario
- Control acceso/permisos
- Programación de tareas
- Gestión inventarios
- Consultar estado ejecuciones
- API RESTful!!!!!!

Si deseais montar un entorno de AWX en local, en el siguiente enlace se explica como realizarlo en local.

https://github.com/ansible/awx/tree/devel/tools/docker-compose#clean-and-build-ui
