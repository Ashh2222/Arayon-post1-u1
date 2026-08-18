# Análisis 2: Petición GET — API REST (jsonplaceholder.typicode.com)

## Petición exitosa — /posts/1

### Información general
- URL: https://jsonplaceholder.typicode.com/posts/1
- Método: GET
- Código de estado: 200 OK
- Remote Address: 172.67.167.151:443

### Headers de Request
| Header | Valor |
|--------|-------|
| :authority (Host) | jsonplaceholder.typicode.com |
| User-Agent | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |
| Accept-Encoding | gzip, deflate, br, zstd |
| Accept-Language | es-US,es-419;q=0.9,es;q=0.8,en;q=0.7 |
| Cache-Control | no-cache |
| Pragma | no-cache |

### Headers de Response
| Header | Valor | Significado |
|--------|-------|--------------|
| Content-Type | application/json; charset=utf-8 | Indica que el cuerpo de la respuesta es JSON, a diferencia del text/html de una página web tradicional |
| Cache-Control | max-age=43200 | Define que el recurso puede considerarse fresco en caché durante 43200 segundos (12 horas) |
| Cf-Cache-Status | HIT | Indica que Cloudflare encontró el recurso disponible en su caché y participó en la entrega de la respuesta |
| Age | 17293 | Segundos transcurridos desde que el recurso fue generado o validado en la caché de Cloudflare |
| Etag | W/"124-yiKdLzqO5gfBrJFrcdJ8Yq0LGnU" | Identificador de esta versión del recurso, usado para validaciones condicionales futuras |
| Server | cloudflare | Infraestructura que atendió la petición en el borde de la red |
| X-Powered-By | Express | Indica que el backend de la API está construido con el framework Express (Node.js) |
| Via | 2.0 heroku-router | Muestra que la petición pasó por el enrutador de Heroku, donde está alojado el backend |
| X-Ratelimit-Limit / Remaining | 1000 / 999 | Límite de peticiones permitidas y las restantes antes de ser bloqueado (rate limiting) |

### Cuerpo de la respuesta (JSON)
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

## Petición fallida — /posts/999

### Información general
- URL: https://jsonplaceholder.typicode.com/posts/999
- Método: GET
- Código de estado: 404 Not Found
- Remote Address: 172.67.167.151:443

### Headers de Response relevantes
| Header | Valor | Significado |
|--------|-------|--------------|
| Content-Type | application/json; charset=utf-8 | La respuesta sigue siendo JSON, incluso al fallar la búsqueda del recurso |
| Content-Length | 2 | El cuerpo de la respuesta ocupa solo 2 bytes, correspondientes a `{}` |
| Cache-Control | max-age=43200 | Incluso una respuesta 404 puede cachearse; aquí se indica un tiempo de frescura de 12 horas |
| Cf-Cache-Status | HIT | Cloudflare encontró esta respuesta 404 ya almacenada en su caché |
| Etag | W/"2-vyGp6PvFo4RvsFtPolWeCReylC8" | Identificador de esta versión específica de la respuesta (incluida la de error) |

### Cuerpo de la respuesta
```json
{}
```
Un objeto JSON vacío: la API confirma que la petición fue procesada correctamente a nivel de servidor, pero no existe ningún recurso con `id = 999`.

## Comparación: petición HTML (Análisis 1) vs petición API REST (Análisis 2)

| Aspecto | GET a example.com (HTML) | GET a /posts/1 (200) | GET a /posts/999 (404) |
|---------|---------------------------|------------------------|---------------------------|
| Content-Type | No visible en la captura, pero corresponde a una página HTML | application/json; charset=utf-8 | application/json; charset=utf-8 |
| Formato del cuerpo | Documento HTML con etiquetas y texto | Objeto JSON estructurado con pares clave-valor | Objeto JSON vacío `{}` |
| Propósito | Renderizar contenido visual en el navegador | Proveer datos consumibles por cualquier cliente (app, script, otra API) | Informar que el recurso solicitado no existe |
| Código de estado observado | 304 Not Modified (recurso en caché) | 200 OK (recurso servido con éxito) | 404 Not Found (recurso inexistente) |
| Infraestructura evidenciada | Cloudflare (CDN) | Cloudflare (CDN) + Heroku (backend) + Express (framework) | Cloudflare (CDN) + Heroku (backend) + Express (framework) |

## Conclusión
Esta comparación evidencia una diferencia clave entre servir una página web y consumir una API REST: mientras example.com devuelve HTML pensado para ser renderizado visualmente por un navegador, jsonplaceholder.typicode.com devuelve JSON, un formato de datos estructurado y ligero pensado para ser procesado por código. La petición a /posts/1 respondió con 200 OK y el objeto completo del recurso solicitado, mientras que /posts/999 respondió con 404 Not Found y un cuerpo JSON vacío (`{}`), manteniendo el mismo Content-Type en ambos casos. Esto demuestra que el código de estado HTTP, no el formato del cuerpo, es el mecanismo principal que indica a un cliente si la operación tuvo éxito o no; un cliente bien diseñado debe verificar siempre el código de estado antes de intentar procesar el cuerpo de la respuesta. También resulta interesante que incluso una respuesta 404 incluya headers de caché (Cache-Control, Cf-Cache-Status, Etag), lo que muestra que Cloudflare trata las respuestas de error igual que cualquier otro recurso cacheable. En conjunto, este análisis refuerza la importancia de los códigos de estado y el header Content-Type como los dos elementos que un cliente HTTP debe inspeccionar primero al recibir cualquier respuesta.