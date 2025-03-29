# QUARKUS - INYECCIÓN DE DEPENDENCIAS (DI)

[← Regresar a notas](../../README.md) <br>

---

Quarkus al ser un producto compatible de Microprofile implementa la especificación CDI.

## Arc
- Quarkus utiliza su propia implementación ligera de CDI llamada Arc.
- Arc está diseñado para ser rápido y eficiente en términos de memoria (crítico en microservicios y nube).
- Está optimizado para el modelo de programación reactivo y tiempos de arranque rápidos.

![DI](./resources/cdi-jakarta-ee.png)

---

## Ejecutar aplicaciones Quarkus desde IntelliJ IDEA

- Instale el plugin `Quarkus Run Configs`

![DI](./resources/quarkus-run-configs.png)

- Seleccione `Edit configuration`

![DI](./resources/edit-configurations.png)

- Agregue una nueva configuración para Quarkus con Maven

![DI](./resources/quarkus-maven-configuration.png)

- Configure el proyecto
```
clean compile quarkus:dev
```

![DI](./resources/quarkus-configuration.png)