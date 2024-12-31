# MAVEN

[← Regresar a notas](../../README.md) <br>

---

> Maven es una herramienta de gestión de dependencias y automatización de construcción para proyectos Java.

## Conceptos clave

> #### [Repositorio central de Maven](https://mvnrepository.com/)
> Es el repositorio público donde se almacenan bibliotecas y dependencias utilizadas en proyectos Maven.
> 
>
> <img src="../resources/images/16-maven/central-mvn-repository.png" width="300" height="200">

> #### Archivo `pom.xml`
> Es el archivo de configuración principal de Maven para cualquier proyecto.
>
> <img src="../resources/images/16-maven/pom.png" width="420" height="300">
>
> > `<groupId>`: Grupo al que pertenece el artefacto.
> 
> > `<artifactId>`: Nombre del artefacto.
> 
> > `<version>`: Versión del artefacto.
> 
> > `<dependencies>`: Maven descargará las dependencias que el proyecto necesita desde el repositorio central de Maven y las almacenará en el directorio `📁.m2/repository`.

> #### Directorio `.m2`
> Es un directorio en el sistema de archivos que contiene:
>   - **Carpeta `📁repository`**: Repositorio local que almacena las dependencias descargadas y puedan ser <u>reutilizadas</u>.
>   - **Archivo `📄settings.xml`**: Archivo de configuración global de Maven (credenciales, repositorios remotos personalizados, etc).
>
> <img src="../resources/images/16-maven/.m2.png" width="350" height="120">


> #### Directorio target
> - Es el directorio de salida donde Maven coloca los archivos generados durante el proceso de construcción del proyecto.
> - Contiene artefactos como el bytecode `.class` y el archivo empaquetado final `.jar` o `.war`.
>
> <img src="../resources/images/16-maven/.jar.png" width="350" height="300">




## Ciclo de vida
El ciclo de vida principal de Maven consta de varias etapas. Las más importantes son:

> `validate`: Verifica que el proyecto esté correctamente configurado y que todas las dependencias necesarias estén disponibles.

> `compile`: Compila el código fuente del proyecto y genera el bytecode en el directorio `target/classes`.

> `test`: Ejecuta pruebas unitarias. Los resultados se encuentran en `target/surefire-reports`.

> `package`: Empaqueta el proyecto en su formato final `jar` o `war`.

> `verify`: Verifica que el artefacto empaquetado cumpla con los criterios de calidad configurados.

> `install`: Instala el artefacto en el repositorio local `./m2/repository` para que pueda ser utilizado por otros proyectos.

> `deploy`: Publica el artefacto en un repositorio remoto para compartirlo con otros desarrolladores o sistemas.

> <img src="../resources/images/16-maven/maven-lifecycle.png" width="700" height="125">


## Comando básico
```sh
  mvn clean install
```

- `clean`: Limpia el directorio `target` antes de realizar cualquier acción.
- `install`: Ejecuta todas las fases necesarias hasta `install`.

> 📌 Aunque `clean` no forma parte del ciclo de vida de Maven, suele usarse junto a él para garantizar un entorno limpio antes de compilar el proyecto.
