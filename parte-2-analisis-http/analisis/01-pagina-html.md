# Análisis 1: Petición GET — example.com

## Información general
- URL: https://example.com/
- Método: GET
- Código de estado: 304 Not Modified

## Headers de Request
| Header | Valor |
|--------|-------|
| :authority | example.com |
| User-Agent | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36 |
| Accept | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 |
| Accept-Encoding | gzip, deflate, br, zstd |
| Accept-Language | es-ES,es;q=0.9 |
| Cache-Control | max-age=0 |
| If-Modified-Since | Wed, 12 Aug 2026 20:15:57 GMT |

## Headers de Response
| Header | Valor | Significado |
|--------|-------|-------------|
| Content-Type | No visible en los Response Headers capturados | Indica el tipo de contenido de la respuesta, pero no se documenta un valor que no haya sido observado directamente |
| Cache-Control | (no capturado — revisar Response Headers) | Define las reglas de cacheo del recurso en el cliente |
| Age | 12189 | Segundos que han pasado desde que el recurso fue generado o validado en el servidor/CDN |
| Cf-Cache-Status | HIT | Indica que Cloudflare encontró el recurso disponible en su caché y participó en la entrega de la respuesta |
| Etag | "6a7cd47d-22f" | Identificador único de esta versión del recurso, usado para validar si cambió desde la última visita |
| Last-Modified | Wed, 12 Aug 2026 20:15:57 GMT | Fecha de la última modificación del recurso en el servidor |
| Server | cloudflare | Software/infraestructura que atendió la petición |

## Tiempos de carga
| Fase | Tiempo (ms) |
|------|------------|
| Queueing | 0.56 ms |
| Stalled (Connection Start) | 0.79 ms |
| DNS Lookup / Initial connection / SSL | No aparecen — el navegador reutilizó una conexión TCP/TLS ya establecida |
| Request sent | 0.23 ms |
| TTFB (Waiting for server response) | 103.69 ms |
| Content Download | 0.29 ms |
| **Total** | **105.56 ms** |

## Conclusión
La petición GET a example.com devolvió un código 304 Not Modified en lugar de 200 OK. La respuesta 304 indica que el recurso no necesitaba ser transferido nuevamente porque la representación almacenada en caché seguía siendo válida, validación que se realizó mediante el header If-Modified-Since enviado en la solicitud junto con el Etag y Last-Modified del recurso. Esto demuestra el mecanismo de caché condicional de HTTP, que evita transferir de nuevo el cuerpo completo del recurso y ahorra ancho de banda. Los headers de respuesta muestran además que el sitio está detrás de Cloudflare (Server: cloudflare, Cf-Cache-Status: HIT), lo que indica que Cloudflare encontró el recurso en su caché y participó en la entrega de la respuesta. El tiempo total de la petición fue de apenas 105.56 ms, dominado casi por completo por la fase de "Waiting for server response" (103.69 ms, aproximadamente el 98.2% del total), mientras que las fases de conexión (DNS, TCP, TLS) no aparecieron por reutilizarse una conexión ya activa, lo que aceleró considerablemente la carga. El cuerpo de la respuesta confirma que se trata de una página HTML simple y estática, coherente con el propósito documentado del dominio ("This domain is for use in documentation examples"). En conjunto, esta petición evidencia cómo HTTP optimiza cargas repetidas mediante cabeceras condicionales y reutilización de conexiones, en lugar de transferir contenido y reestablecer conexiones innecesariamente.