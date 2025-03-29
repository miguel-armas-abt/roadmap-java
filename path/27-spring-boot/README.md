# Spring Boot

[← Regresar a notas](../../README.md) <br>

---

## 1. Spring Framework
> Spring framework es un conjunto de herramientas para escribir aplicaciones Java, que nos ofrece un conjunto de plantillas
> predefinidas para las principales funcionalidades, como seguridad, persistencia, MVC y demás.

## 2. Spring Boot
> Por otra parte, Spring Boot es una extensión de Spring Framework que incluye un servidor Tomcat embebido y nos libera
> de todas las tareas repetitivas de configuración, debido a la gran cantidad de **starters** con todas las características
> necesarias para llevar a cabo ciertas tareas. Por ejemplo, el starter web trae el Tomcat embebido para desplegar una 
> aplicación web de manera sencilla. Así mismo, el starter JPA tiene las preconfiguraciones para trabajar con una base de datos.

## 3. Inyección de dependencias con Spring Boot

> 1. `Beans`: Representan a los objetos que son instanciados, configurados y destruidos por el contenedor de Spring (dependencias).
> 2. `Estereotipos`: Anotaciones que especifican al contenedor de Spring el rol y propósito de los bean dentro de la aplicación.
> 3. `Contenedor de Spring`: Infraestructura fundamental de Spring que gestiona la creación, configuración y ciclo de vida de los beans.

Spring Boot utiliza `estereotipos` para definir los `beans` gestionados por el `contenedor de Spring`.

| Estereotipos      | Descripción                                                                                                                                      |  
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `@Bean`           | Define un método que produce un bean para ser gestionado por el contenedor de Spring.                                                            |
| `@Configuration`  | Indica que una clase contiene métodos `@Bean` y puede ser procesada por el contenedor de Spring para generar definiciones de beans.              |
| `@Component`      | Marca una clase como un componente genérico y candidato para ser detectado automáticamente y registrado como un bean en el contenedor de Spring. |
| `@Service`        | Especialización de `@Component` que indica que una clase proporciona lógica de negocio.                                                          |
| `@Repository`     | Especialización de `@Component` que indica que una clase accede a la base de datos o a una fuente de datos.                                      |
| `@RestController` | Especialización de `@Component` que define un controlador REST.                                                                                  |

```java
@RestController
public class ProductController {
 
    private final ProductService productService;
    
    public ProductController(ProductService productService) {
        this.productService = productService;
    }
}
```

```java
@Service
public class ProductService {
    
    private final ProductRepository productRepository;
    
    public ProductService(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }
}
```

```java
@Repository
public class ProductRepository {

    private final RestTemplate restTemplate;
    
    public ProductRepository(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }
}
```

```java
@Configuration
public class RestTemplateConfig {
  
  @Bean
  public RestTemplate restTemplate() {
    return new RestTemplate();
  }
}
```

## 4. Inyección automática
Spring Boot brinda las siguientes anotaciones para inyectar beans, permitiendo la resolución automática de dependencias.

| Anotación        | Descripción                                                                                                                 |  
|------------------|-----------------------------------------------------------------------------------------------------------------------------|
| `@Autowired`     | Indica que una dependencia debe ser inyectada automáticamente por Spring. Se puede usar en constructores, métodos y campos. |
| `@Qualifier`     | Utilizada junto con `@Autowired` para especificar qué bean debe ser inyectado cuando hay múltiples candidatos disponibles.  |

```java
@Service
public class ProductService {
  
  @Autowired
  private ProductRepository productRepository;

}
```

# 5. Tipos de contenedores
> - `BeanFactory`: Contenedor simple con soporte básico para inyección de dependencias.
> - `ApplicationContext`: Contenedor que extiende `BeanFactory` e incluye capacidades adicionales, tales como:
>     - Soporte para publicar y suscribir eventos dentro de la aplicación.
>     - Carga de beans desde archivos de configuración o a través de `@Configuration`.
>     - Integración con Programación Orientada a Aspectos (AOP).
> 
> En la práctica `ApplicationContext` es la elección predeterminada debido a su robustez, mientras que `BeanFactory` se
> utiliza cuando se requiere un contenedor extremadamente ligero (applets, apps moviles, etc).
