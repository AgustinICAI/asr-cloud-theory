# 3. Cloud Computing

### 3.7 Estimación de costes Cloud. Migración.

El término ***migración cloud*** (o *cloud migration*) se refiere al proceso completo mediante el cual una empresa mueve algunas de (o todas) las capacidades de su Data Center (DC) propio a la nube. Normalmente este término se suele usar cuando se refieren a una nube pública, no privada, aunque sería aplicable a cualquier tipo de nube por supuesto.  Pero, ¿cuáles son los principales beneficios de la nube (si es que aún no nos han quedado del todo claros)?

Como hemos comentado anteriormente, algunos de los principales beneficios de usar recursos en la nube pública son:

* **Escalabilidad**: No nos debería quedar ninguna duda en este momento que la nube nos ofrece una capacidad de escalado vertical y horizontal que puede ser explotado muy beneficiosamente para los incrementos de cargas de trabajo de una compañía. Además de la capacidad de escalado tan grande que nos ofrece, la nube suele acompañar esta beneficiosa característica del hecho de hacerlo de una forma muy sencilla (*user friendly*) casi sin ningún esfuerzo. Hemos visto recientemente ejemplos en los que el "casi ningún" se convierte literalmente en "cero" esfuerzos, e.g. las FaaS. 
* **Coste**: Uno de los costes que principalmente impulsaron el uso de la nube fue precisamente el coste. El hecho de que la nube nos oferte la posibilidad de diseñar arquitecturas completamente **serverless**, junto con el modelo de pago que ellas promueven (paga por lo que usas, o **PAYG** del inglés *pay as you go* ), evidentemente da como resultado la posibilidad de reducir costes comparado con una infraestructura tecnológica clásica basada en servidores locales, en las cuales las compañías tenían que tener un gasto inicial y posterior recurrente de adquisición de los servidores físicos, licencias de software, almacenamiento, redes, etc. además de su mantenimiento, actualizaciones y "parcheos" de seguridad continuos. El eliminar este recurrente y estrés de equipos tecnológicos locales, delegando la responsabilidad en el proveedor de la nube, ha resultado en la posibilidad de una mayor inversión en innovación, que a su vez ha repercutido en reducción de costes y aumento de valoración de muchas compañías, que se han reconvertido como tecnológicas.
* **Rendimiento**: Como también hemos experimentado en algunos de nuestros quicklabs, la alta resiliencia ofertada por las nubes líderes, así como su eficiencia en la gestión del tráfico y el escalado, derívale en una mejora del rendimiento de muchos aplicativos (como por ejemplo web oficiales) que finalmente tienen un impacto en la marca. Esto no se debe sólo al escalado, sino a la facilidad de realización de nuestras aplicaciones y websites en regiones mundiales más cercanas al usuario, reduciendo así latencias y minimizando el riesgo de que una caída local afecte al servicio a nivel internacional. 
* **Experiencia digital:** Los usuarios de la nube no están restringidos a una geografía para acceder a los servicios de la misma. Y, aunque muchas compañías han invertido bastante en la extensión de sus redes locales a través de VPNs a nivel mundial para sus trabajadores, hemos visto que la creación y gestión de redes no solo es user-friendly, sino que tienen apalancamiento en sistemas de autenticación lideres a nivel mundial, con políticas de actualización transparentes y al día. Todo esto no solo aplica a los empleados, sino también a clientes de la propia empresa. Todo ello ha empujado fuertemente lo que ya se conoce en la industria como *revolución digital*, mejorando la experiencia de usuarios y clientes, además de tener un impacto en la operabilidad y rendimiento de los propios empleados.

La mayoría de estas ideas están reflejadas en un manifiesto que se ha convertido en un estándar, **[las 10 leyes de cloud-economics](http://www.virtualdensity.com/resources/the-10-laws-of-cloudonomics/)**. 

#### *Cloud economics*: Las 10 leyes

Sorprendentemente, las *10 leyes* no son algo reciente, sino que fueron [*enunciadas* en 2008 por Joe Weinman](http://www.joeweinman.com/Resources/Joe_Weinman%2010%20Laws%20of%20Fogonomics.pdf), por entonces "Strategic Solutions Sales VP" en AT&T Global Business Services. 

1. **Utility Services Cost Less Even Though They Cost More** (Los servicios públicos cuestan menos aunque cuestan más): Incluso si los costos unitarios de los recursos de la nube pública son más altos que los privados, el precio de pago por uso en presencia de una demanda variable puede hacer que el costo total sea más bajo. Dependiendo de las diferencias en los precios, la variabilidad de la demanda de la carga de trabajo y las diferencias de rendimiento, las nubes híbridas a menudo pueden minimizar los costos totales.
2. **On-Demand Trumps Forecasting** (La gestión a demanda supera con creces las estimaciones generales): no importa como de buena sea la previsión de la demanda de la carga de trabajo, el aprovisionamiento de recursos casi a tiempo real (on-demand) será siempre mejor al capturar exactamente el binomio capacidad-demanda. Esto solo se puede hacer económicamente en una nube pública con recursos compartidos asignados dinámicamente.  
3. **The Peak of The Sum Is Never Greater Than the Sum of the Peaks** (El pico de la suma nunca superará la suma de los picos): La capacidad agregada necesaria en un conjunto dinámico de recursos compartidos es normalmente inferior, o en el peor de los casos igual, a la capacidad necesaria cuando ésta en nubes privadas en silos. En práctica esto se puede visualizar tal y como sigue: Una empresa desarrolla su capacidad para manejar sus picos de demanda. Las empresas que se dediquen a consultoría financiera, por ejemplo, tendrá su pico el 15 de abril, unos grandes almacenes, el Black Friday, etc. Un proveedor Cloud aplanará la curva de demanda agregando todos los tipos de tráfico   
4. **Aggregate Demand Is Smoother Than Individual** (La demanda agregada es más suave que la individual): En otras palabras, el coeficiente de variación (la división entre la desviación estándar y la media, $c_v=\frac{\sigma}{|\overline{x}|}$) de una suma de múltiples variables aleatorias independientes distribuidas de manera idéntica (que representan niveles de demanda de carga de trabajo individual) con medias y varianzas distintas de cero es menos que la de cualquier individuo.
5. **Average Unit Costs Are Reduced by Distributing Fixed Costs Over More Units of Output** (Los costos unitarios promedio se reducen al distribuir los costos fijos entre más unidades):  Las economías de escala se aplican a los proveedores de nube pública que operan centros de datos con cientos de miles de servidores.
6. **Superiority in Numbers Is the Most Important Factor in The Result of a Combat** (La superioridad en números es el factor más importante en el resultado de un combate) - Carlvon Clausewitz: Las nubes públicas tienen infraestructuras masivas y mejor preparadas que las que se podrían tener a nivel individual, disminuyendo así el riesgo de verse afectadas por ciberataques como botnets que generan un ancho de banda masivo de ataques de denegación de servicio (DoS) distribuidos.
7. **Space-Time Is a Continuum** (El espacio-tiempo es un continuo) - Albert Einstein / Hermann Minkowski: Aplicaciones o tareas masivamente paralelas (e.g., la fase Map en trabajos MapReduce) pueden compensar el número de procesadores por el tiempo de computación. En presencia de precios de pago por uso, esto significa que la aceleración es gratuita. 
8. **Dispersion Is the Inverse Square of Latency** (La dispersión es el cuadrado inverso de la latencia): Se necesitan cuatro veces más nodos para reducir la latencia a la mitad en una superficie como un plano, por lo que eventualmente la reducción de la latencia se vuelve prohibitivamente costosa.  $\text{Latencia}=1/\sqrt{\text{nodos}}$.
9. **Don’t Put All Your Eggs in One Basket** (No pongas todos tus huevos en la misma canasta): Mientras que un solo data center empresarial está en riesgo de un desastre natural, e incluso un sitio hermano cercano puede ser destruido por el mismo desastre, por ejemplo, una inundación, un tornado o un huracán, una nube que ofrece muchas zonas y regiones de disponibilidad, cada una con buena confiabilidad, puede crear una arquitectura de sistema con mucha más resistencia al fallo general por desastre. La disponibilidad de un sistema con redundancia *n* es de *1-(1-d)n*. Así, si la disponibilidad de un Datacenter es del 99%, la de dos será de 99,99% y de 3 Datacenters 99,9999%. 
10. **An Object at Rest Tends to Stay at Rest** (Un objeto en reposo tiende a permanecer en reposo) - Isaac Newton: Una empresa privada tiende a implantar su infraestructura donde se encuentra la empresa. Un gran Data Center elige la ubicación según muchos parámetros como hemos visto en la primera parte de la asignatura.



#### Retos de una migración cloud

A pesar de todas sus ventajas mencionadas tanto a presente como a futuro, cualquier migración cloud conlleva unos riesgos, que normalmente escalan con el *legacy tecnológico* de la empresa (lo cual suele escalar con la edad de la misma). Las migraciones cloud pueden llegar a ser maniobras muy complejas y arriesgadas por diversas razones. Los principales retos reportados en migraciones de este tipo son:

**Falta de un plan estratégico a nivel compañía**

Muchas organizaciones se deciden a una migración a la nube sin haber empleado un esfuerzo inicial necesario en el diseño de una estrategia clara, dividida en objetivos realistas y realizables en los tiempos necesarios. Una migración con éxito require una planificación exhaustiva, lo que conlleva un conocimiento profundo de todos los componentes tecnológicos de la organización, y la elaboración de un plan detallado (priorizado según la complejidad de las interrelaciones de los diferentes componentes tecnológicos). Susodicho plan no solo tiene que existir en papel, sino que debe tener un claro apoyo por la organización, lo cual no es posible sin la elaboración conjunta de un "Caso de Negocio", que apoye con razones pormenorizadas la  decisión de la migración de un componente a la nube. 

**Mala gestión de los objetivos y malentendidos de costes**

Al migrar a la nube, muchas organizaciones no han establecido KPI claros para comprender lo que planean gastar o ahorrar después de la migración. Esto hace que sea difícil entender si la migración tuvo éxito, desde un punto de vista económico. Además, los entornos en la nube son dinámicos y los costos pueden cambiar rápidamente a medida que se adoptan nuevos servicios y aumenta el uso de las aplicaciones.

**Vendor Lock-In**

El vendor lock-in es un problema común para los que adoptan la tecnología cloud. Los proveedores cloud, como hemos visto en este curso, ofrecen una gran variedad de servicios, pero muchos de ellos no pueden extenderse a otras plataformas en la nube. La migración de cargas de trabajo de una nube a otra es un proceso largo y costoso. Muchas organizaciones comienzan a utilizar servicios en la nube y luego les resulta difícil cambiar de proveedor si el proveedor actual no se adapta a sus requisitos.

**Data security & Compliance**

Uno de los principales obstáculos para la migración a la nube es la *seguridad* de los datos y el *cumplimiento* con las legislaciones activas (*compliance*). Los servicios cloud utilizan un modelo de responsabilidad compartida, en el que asumen la responsabilidad de proteger la infraestructura y el cliente es responsable de proteger los datos y las cargas de trabajo. Por lo tanto, si bien el proveedor de la nube puede proporcionar medidas de seguridad sólidas, es responsabilidad de su organización configurarlas correctamente y asegurarse de que todos los servicios y aplicaciones tengan los controles de seguridad adecuados. El proceso de migración en sí mismo presenta riesgos de seguridad. La transferencia de grandes volúmenes de datos, que pueden ser confidenciales, y la configuración de controles de acceso para aplicaciones en diferentes entornos, crea una exposición significativa.

#### Estrategias de migración

Una migración cloud debe considerar qué estrategia responde mejor a las necesidades de la organización. A continuación podemos ver algunas de las más frecuentes (las 5Rs): 

* **Rehost**: La reubicación, o "elevación y cambio" (lift-and-shift), implica el uso de infraestructura como servicio (IaaS). Esta estrategia se centra en volver a implementar los datos y aplicaciones existentes en el la nube pública, sin hacer ningún cambio a nivel programático. Es la más fácil de las opciones, y es por lo que es adecuado para organizaciones menos familiarizadas con los entornos de nube. También es una buena opción para los casos en los que es difícil modificar el código y hay necesidades de migrar sus aplicaciones intactas. 
* **Refactorizar**: Refactorizar, o "levantar, retocar y cambiar" (lift-tinker-and-shift), es cuando se modifican y optimizan las aplicaciones para el entorno cloud. En este caso, se emplea un modelo de plataforma como servicio (PaaS). La arquitectura central de las aplicaciones permanece sin cambios, pero se realizan ajustes para permitir un mejor uso de las herramientas basadas en la nube. 
* **Revisión**: se basa en las estrategias anteriores, requieriendo más cambios significativos en la arquitectura y el código de los sistemas que se trasladan a la nube. Esto se hace para permitir que las aplicaciones aprovechen al máximo los servicios disponibles en la nube, lo que puede requerir la introducción de cambios importantes en el código. Esta estrategia requiere planificación anticipada y conocimientos avanzados. 
* **Reconstruir**: La reconstrucción lleva el enfoque Revise aún más lejos al descartar el código base existente y reemplazarlo por uno nuevo. Este proceso lleva mucho tiempo y solo se considera cuando las empresas deciden que sus soluciones existentes no satisfacen las necesidades comerciales actuales. 
* **Reemplazar**: Reemplazar es otro enfoque de reinvención como en el Reconstruir. La diferencia aquí es que la empresa no vuelve a desarrollar su propia aplicación nativa desde cero. Esto implica migrar a una aplicación prediseñada de terceros proporcionada por el proveedor. Lo único que migra de su aplicación existente son los datos, mientras que todo lo demás sobre el sistema es nuevo.

#### Estimación de costes

Tenidas en cuenta todas las consideraciones que hemos estado comentando hasta ahora, sin duda alguna un componente importante de una migración cloud es la estimación de costes en los que incurriremos en el caso de decidirnos por un recurso u otro. Para ello, cada nube pone a nuestro servicio un estimador de los costes asociados, por lo general considerando las siguientes características (y algunas otras más específicas):

* Capacidad de cómputo
* Capacidad de almacenamiento
* Tiempo medio de uso al día
* Número medio de ejecuciones al día
* Región de cómputo

Estas calculadoras de estimación las podemos encontrar en los siguientes links:

* Google cloud [calculator](https://cloud.google.com/products/calculator)
* AWS [calculator](https://calculator.aws/#/)
* Microsoft Azure [calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
* IBM [calculator](https://www.ibm.com/cloud/cloud-calculator)

Sin embargo, no todos los costes de una migración estarán relacionados con los recursos cloud per sé. Entre otras cosas, una migración de este tipo requiere de perfiles especializados, que pueden incluir entre otros:

* **Desarrollador cloud** (Cloud Developer): Expertos en la materia de diseño, construcción, prueba y mantenimiento de aplicaciones y servicios en la nube. Las responsabilidades de este rol incluyen participar en todas las fases del desarrollo: desde los requisitos, la definición y el diseño; al desarrollo, despliegue y mantenimiento; incluyendo el ajuste y la supervisión del rendimiento de los servicios.
* **Arquitecto cloud** (Cloud Architect): Tienen conocimiento profundo de la arquitectura cloud, diseñan, desarrollan y administran soluciones sólidas, seguras, escalables, de alta disponibilidad y dinámicas para impulsar los objetivos de la organización. Un arquitecto cloud tiene como responsabilidad principal la de convertir los requerimientos técnicos de un proyecto en la arquitectura y diseño que guiará el producto final. Suelen tener un buen conocimiento de sistemas operativos, buen entendimiento de sistemas en red, varios lenguajes de programación (C, Java, Python, etc.), y un conocimiento fundamental de los conceptos de seguridad cloud. 
* **Administrador cloud** (Cloud Admin): Un administrador cloud planifica, configura y administra las cargas de trabajo en la nube. Las habilidades específicas necesarias para el día a día de este rol pueden variar de una empresa a otra. En algunas organizaciones, los cloud admins pueden diseñar arquitecturas y estrategias de la nube, mientras que en las empresas más grandes esas tareas suelen ser manejadas por un arquitectos cloud.
* **Ciberseguridad cloud** (Cloud Security Engineers): Un ingeniero de seguridad cloud crea, mantiene, actualiza y mejora continuamente las redes y los servicios cloud-native de una organización. Son responsables de la operación segura de la infraestructura, las plataformas y el software. Instalan, mantienen y actualizan los entornos de computación cloud y la infraestructura central de la organización.