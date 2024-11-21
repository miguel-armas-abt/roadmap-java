# ARQUITECTURA DE PAQUETES

[← Regresar a notas](../../README.md) <br>

---

> La arquitectura de paquetes se refiere a la organización de las clases en módulos dentro de una aplicación de software.

<img src="../resources/images/package-architecture/package-architecture.svg" width="420" height="420">

```
  com.bcp.yape.transfers:
  ├───commons
  ├───dto
  ├───mapper
  ├───router
  ├───service
  ├───repository
  ├───dao
  └─── ...
```

> Si la aplicación tiene más de un dominio, es recomendable dividir la arquitectura de paquetes por cada dominio.

```
  com.bcp.yape.transfers:
  ├───commons
  └───entrypoint
      ├───own
      │   ├───dto
      │   ├───mapper
      │   ├───router
      │   ├───service
      │   ├───repository
      │   └───dao
      │
      └───third
          ├───dto
          ├───mapper
          ├───router
          ├───service
          ├───repository
          └───dao
```