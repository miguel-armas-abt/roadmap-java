# PRUEBAS UNITARIAS

[← Regresar a notas](../../README.md) <br>

---

## 1. Conceptos Clave

> #### Unit Testing
> Pruebas unitarias que verifican el comportamiento de componentes individuales de manera aislada, garantizando que cada unidad de código funcione según lo esperado.

> #### Mock
> Objeto simulado que imita el comportamiento de una dependencia real, permitiendo controlar su respuesta y aislar la unidad en prueba.  
> *Ejemplo: Usar Mockito para simular la respuesta de un repositorio.*

> #### Stub
> Implementación mínima que devuelve datos predefinidos, utilizada para sustituir comportamientos en pruebas unitarias.

> #### JUnit
> Framework de pruebas en Java que proporciona anotaciones (como `@Test`, `@BeforeEach`) y aserciones (como `assertEquals`, `assertTrue`) para validar el comportamiento del código.

> #### Mockito
> Biblioteca de mocking para Java que permite crear y configurar mocks de forma sencilla, facilitando la prueba de unidades en aislamiento.

---

## 2. Pruebas unitarias sin mocks

Cuando se prueba una utilidad que no depende de otras clases, se pueden utilizar pruebas parametrizadas. Por ejemplo, usando **ParameterizedTest** y **CsvSource**:

```java
public class StringUtilTest {

  @ParameterizedTest
  @CsvSource({
    "'hello', 'HELLO'",
    "'world', 'WORLD'",
    "'java', 'JAVA'"
  })
  void testToUpperCase(String input, String expected) {
    // Act
    String result = input.toUpperCase();
    
    // Assert
    assertEquals(expected, result);
  }
}
```

En este ejemplo, se prueba el método toUpperCase() para distintos valores sin utilizar mocks, validando directamente la transformación del texto.

## 2. Pruebas unitarias con mocks

Para probar una lógica que depende de otras capas, se pueden utilizar mocks para aislar la unidad bajo prueba. Por ejemplo, para probar el ProductService se simula la respuesta de ProductRepository.

```java
public class ProductServiceTest {

  @Mock
  private ProductRepository productRepository;
  
  @InjectMocks
  private ProductService productService;
  
  @BeforeEach
  void setUp() {
    MockitoAnnotations.openMocks(this);
  }
  
  @Test
  void testGetProductById() {
    // Arrange: Se simula la respuesta del repositorio
    Product product = new Product(1L, "Laptop", 1500.0);
    when(productRepository.findById(1L)).thenReturn(Optional.of(product));
    
    // Act: Se invoca el método a probar
    Product result = productService.getProductById(1L);
    
    // Assert: Se verifica que el producto devuelto sea el esperado
    assertNotNull(result);
    assertEquals("Laptop", result.getName());
  }
}
```
