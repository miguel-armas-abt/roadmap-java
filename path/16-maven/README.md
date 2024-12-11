# MAVEN

[← Regresar a notas](../../README.md) <br>

---

> Maven es una herramienta de gestión de dependencias y automatización de construcción para proyectos Java.

## Conceptos clave

> #### Directorio target
> - Es el directorio de salida donde Maven coloca los archivos generados durante el proceso de construcción.
> - Contiene artefactos como el bytecode `.class` y el archivo empaquetado final `.jar` o `.war`.
>
> <img src="../resources/images/16-maven/.jar.png" width="350" height="300">

> #### Directorio `.m2`
> - Es un directorio en el sistema operativo que contiene:
>   - **Carpeta `repository`**: Repositorio local que lmacena las dependencias descargadas de los repositorios remotos para su reutilización.
>   - **Archivo `settings.xml`**: Configuración global de Maven (credenciales, repositorios personalizados, etc).
>
> <img src="../resources/images/16-maven/.m2.png" width="350" height="120">

> #### Archivo `pom.xml`
> - Es el archivo de configuración principal de Maven para cualquier proyecto.
> 
> <img src="../resources/images/16-maven/pom.png" width="420" height="300">
> 
> - `groupId`: Grupo al que pertenece el artefacto.
> - `artifactId`: Nombre del artefacto.
> - `version`: Versión del artefacto.
> - `dependencies`: 
>   - Dependencias externas que el proyecto necesita para funcionar.
>   - Maven descargará estas dependencias desde el repositorio central de Maven y las almacenará en el directorio `.m2/repository`.


## Ciclo de vida
El ciclo de vida principal de Maven consta de varias etapas. Las más importantes son:

> #### `validate`
> Verifica que el proyecto esté correctamente configurado y que todas las dependencias necesarias estén disponibles.

> #### `compile`
> Compila el código fuente del proyecto y genera el bytecode en el directorio `target/classes`.

> #### `test`
> Ejecuta pruebas unitarias. Los resultados se encuentran en `target/surefire-reports`.

> #### `package`
> Empaqueta el proyecto en su formato final `jar` o `war`.

> #### `verify`
> Verifica que el artefacto empaquetado cumpla con los criterios de calidad configurados.

> #### `install`
> Instala el artefacto en el repositorio local `./m2/repository` para que pueda ser utilizado por otros proyectos.

> #### `deploy`
> Publica el artefacto en un repositorio remoto para compartirlo con otros desarrolladores o sistemas.

> <img src="../resources/images/16-maven/maven-lifecycle.png" width="700" height="170">


## Comando básico
```sh
  mvn clean install
```

- `clean`: Limpia el directorio `target` antes de realizar cualquier acción.
- `install`: Ejecuta todas las fases necesarias hasta `install`.

> 📌 Aunque `clean` no forma parte del ciclo de vida de Maven, suele usarse junto a él para garantizar un entorno limpio antes de compilar el proyecto.
