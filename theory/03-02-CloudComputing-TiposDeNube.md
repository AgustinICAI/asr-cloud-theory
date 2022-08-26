# 3. Cloud Computing

### 3.2 Tipos de nubes

Existen tres tipos principales de "nube" (cloud computing):

* Nuble pública
* Nube privada
* Nube híbrida

Aunque en ocasiones se incluye también la combinación de todas ellas (**multi-cloud**) como una cuarta variante, la realidad es que es una combinación de las anteriores, por lo que nosotros no haremos susodicha distinción.

En la ***nube pública*** los recursos ofertados por el proveedor externo son gestionados a través de Internet vía aplicaciones o servicios Web. Las nubes públicas son gestionadas por organizaciones externas al consumidor. En este caso, los consumidores no tienen exclusividad de uso de los servidores, almacenamiento y redes del proveedor. Es decir, aplicaciones de diferentes consumidores podrán convivir en un mismo servidor con el fin de optimizar su uso (por parte del proveedor).

En la ***nube privada*** los recursos son de exclusivo uso de un cliente, y son operadas y gestionadas en redes privadas. En éstas, el consumidor tiene total control sobre los datos, la seguridad y la calidad del servicio. Las nubes privadas pueden crearse tanto por el propio departamento de IT de una compañía, como por un proveedor cloud externo.

En la ***nube* *híbrida*** se combinan ambos mundos, parte de la nube será pública, y parte de ella será privada. Este tipo de nube introduce un factor de complejidad adicional, el de la determinación sobre qué ha de ser enviado a la nube pública y qué a la privada. A pesar de ello, este modelo parece ser el más conveniente en organizaciones con una tradición monolítica que busca reducir la deuda tecnológica mediante la migración gradual a la nube pública.

Por último, cabe mencionar el paradigma ***multicloud***. El término [multicloud](https://www.redhat.com/es/topics/cloud-computing/what-is-multicloud) se refiere a un enfoque de nube compuesto por al menos dos servicios de nube, que proporcionan por lo menos dos proveedores de nube pública o privada. Todas las nubes híbridas son multiclouds, pero no todas las multiclouds son híbridas. Las multiclouds se vuelven híbridas cuando se conectan varias nubes con algún tipo de [integración](https://www.redhat.com/es/topics/integration/what-is-integration) u organización.

A modo de resumen:

| Nubes Públicas                                               | Nubes Privadas                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Infraestructura compartida a la que todo el mundo puede acceder | Infraestructura propiedad y accedida por un cliente          |
| Proporciona niveles de HW y virtualización, propiedad del proveedor, compartidos por todos los clientes | Proporciona niveles de HW y virtualización, propiedad del cliente y para su propio uso |
| Recursos “infinitamente” elásticos                           | Recursos elásticos finitos                                   |
| Conectada a la Internet pública                              | Puede o no estar conectada a la Internet pública.            |

### 