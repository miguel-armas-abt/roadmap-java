# EVOLUCIÓN DE LAS ARQUITECTURAS DE DESPLIEGUE PARA APLICACIONES JAVA

## Servidor de aplicaciones tradicional
- Una JVM se instala sobre un SO junto con un servidor de aplicaciones (como Tomcat, WebLogic, JBoss, etc) para ejecutar aplicaciones Java.
- La JVM es crítica pero consume recursos significativos.

![Traditional architecture](./resources/traditional-architecture.png)

## Aplicaciones contenerizadas en servidores
- Docker Engine se instala en el SO para ejecutar contenedores, los cuales son creados con entornos de ejecución aislados del SO.
- Dado que la JVM interpreta el bytecode al código de máquina del SO subyacente, entonces su participación pierde sentido, ya que no hay un SO subyacente dentro de los contenedores.
- Además, la redundancia de múltiples JVMs en contenedores distintos resulta en un uso excesivo de recursos.

![Containerized architecture](./resources/containerized-architecture.png)

##  Aplicaciones contenerizadas en un clúster de Kubernetes
- Kubernetes gestiona un clúster de contenedores, asignando recursos dinámicamente y manejando aplicaciones efímeras.
- La ineficiencia de la JVM se acentúa en este entorno, por lo que se exploran alternativas como <u>GraalVM</u>.

![Containerized arch+k8s](./resources/containerized-arch+k8s.png)