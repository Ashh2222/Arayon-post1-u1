# Análisis 3: Petición POST con Postman

## Configuración de la petición
- Herramienta: Postman
- Método: POST
- URL: https://jsonplaceholder.typicode.com/posts
- Header enviado: `Content-Type: application/json`

### Body enviado (raw / JSON)
```json
{
  "title": "Laboratorio Programacion Web",
  "body": "Analisis de peticiones HTTP con Postman.",
  "userId": 1
}
```

## Respuesta recibida
- Código de estado: **201 Created**
- Tiempo de respuesta: 388 ms
- Tamaño de la respuesta: 1.32 KB

### Cuerpo de la respuesta (JSON)
```json
{
  "title": "Laboratorio Programacion Web",
  "body": "Analisis de peticiones HTTP con Postman.",
  "userId": 1,
  "id": 101
}
```

El servidor devolvió exactamente el mismo objeto enviado, agregando un campo `id: 101` generado automáticamente — así es como una API REST confirma la creación de un nuevo recurso.

## Tests automatizados

```javascript
pm.test("Status 201 Created", () => {
  pm.response.to.have.status(201);
});

pm.test("Respuesta incluye id asignado", () => {
  const json = pm.response.json();
  pm.expect(json).to.have.property("id");
  pm.expect(json.title).to.equal("Laboratorio Programacion Web");
});
```

### Resultado de los tests
| Test | Resultado |
|------|-----------|
| Status 201 Created | ✅ PASSED |
| Respuesta incluye id asignado | ✅ PASSED |

Ambos tests pasaron correctamente: el código de estado fue el esperado (201) y la respuesta incluyó el campo `id` con el valor `title` intacto.

## Comparación: GET vs POST

| Aspecto | GET (Análisis 1 y 2) | POST (este análisis) |
|---------|------------------------|------------------------|
| Propósito | Solicitar/leer un recurso existente | Crear un nuevo recurso en el servidor |
| Cuerpo en la petición (Request Body) | No aplica — GET no envía body | Sí — se envía un objeto JSON con los datos del nuevo recurso |
| Código de estado esperado en éxito | 200 OK (o 304 Not Modified si está en caché) | 201 Created |
| Efecto en el servidor | Ninguno (operación de solo lectura, idempotente) | Modifica el estado del servidor al crear un registro nuevo |
| Identificador del recurso | Ya existe antes de la petición (ej. `/posts/1`) | Se genera y devuelve como parte de la respuesta (`id: 101`) |
| Content-Type relevante | No se envía en la petición (solo en la respuesta) | Se envía explícitamente en la petición para indicar el formato del body |

## Conclusión
Esta petición POST demuestra el ciclo completo de creación de un recurso vía API REST: el cliente envía un objeto JSON en el cuerpo de la petición junto con el header Content-Type: application/json para indicar el formato de los datos, y el servidor responde con 201 Created, devolviendo el mismo objeto enriquecido con un id generado automáticamente. A diferencia de las peticiones GET analizadas anteriormente, que solo solicitan datos existentes sin modificar el estado del servidor, POST provoca un efecto: la creación de un nuevo recurso (aunque en el caso de jsonplaceholder.typicode.com, al ser una API de pruebas, el recurso no persiste realmente). Los tests automatizados en Postman permitieron validar de forma programática tanto el código de estado como la estructura de la respuesta, lo cual es una práctica fundamental al construir integraciones con APIs, ya que evita depender de una inspección manual para confirmar que el comportamiento fue el esperado.