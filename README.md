# Post-contenido — Unidad 1: Fundamentos de la Web

## Descripción
Repositorio del laboratorio de la Unidad 1 de Programación Web. Contiene dos partes: configuración del entorno de desarrollo (`parte-1-entorno/`) y análisis de peticiones HTTP con Chrome DevTools y Postman (`parte-2-analisis-http/`).

## Parte 1 — Entorno de desarrollo

Configuración completa del entorno de trabajo: VS Code con extensiones esenciales (Live Server, Prettier, GitLens, ESLint), Git y GitHub, y una página HTML básica inspeccionada con Chrome DevTools (panel Elements, Console y Network).

### Cómo ejecutar la Parte 1
1. Clonar este repositorio.
2. Abrir la carpeta `parte-1-entorno/` en VS Code.
3. Clic derecho sobre `index.html` → **"Open with Live Server"**.
4. La página se abrirá en el navegador, mostrando un header azul, dos secciones con borde lateral y efecto hover, y un footer oscuro.

Ver `parte-1-entorno/`.

### Evidencias — Parte 1

**Extensiones instaladas en VS Code**
![Extensiones VS Code](parte-1-entorno/capturas-p1/Cap-Extensiones.png)

**Configuración de Git**
![Configuración de Git](parte-1-entorno/capturas-p1/Cap2-Git.png)

**Repositorio creado en GitHub**
![Repositorio en GitHub](parte-1-entorno/capturas-p1/Cap3-Repositorio.png)

**Página HTML renderizada con Live Server**
![Página renderizada](parte-1-entorno/capturas-p1/Cap4-Pagina-v1.png)

**Inspección del DOM con DevTools**
![Inspección DOM](parte-1-entorno/capturas-p1/Cap5-Inspección.png)

**Edición en vivo de estilos con DevTools**
![Edición en vivo](parte-1-entorno/capturas-p1/Cap6-Inspección-edición-en-vivo.png)

**Consola de DevTools con los mensajes de main.js**
![Consola DevTools](parte-1-entorno/capturas-p1/Cap7-Consola.png)

**Historial de commits de la Parte 1**
![Commits Parte 1](parte-1-entorno/capturas-p1/Cap8-Commits.png)

## Parte 2 — Análisis de peticiones HTTP

| # | Tipo | URL | Código |
|---|------|-----|--------|
| 1 | GET HTML | https://example.com | 304 Not Modified |
| 2 | GET JSON (exitoso) | /posts/1 | 200 OK |
| 3 | GET JSON (fallido) | /posts/999 | 404 Not Found |
| 4 | POST JSON | /posts | 201 Created |

Cada petición fue inspeccionada con el panel Network de Chrome DevTools (headers de request/response, tiempos de carga) o con Postman (para el POST, incluyendo tests automatizados). El análisis detallado de cada una está documentado en `parte-2-analisis-http/analisis/`.

Ver `parte-2-analisis-http/analisis/`.

### Evidencias — Análisis 1: GET a example.com
![Análisis 1 - General](parte-2-analisis-http/capturas/cap-analisis1-01.png)
![Análisis 1 - Request Headers](parte-2-analisis-http/capturas/cap-analisis1-02.png)
![Análisis 1 - Headers completos](parte-2-analisis-http/capturas/cap-analisis1-03.png)
![Análisis 1 - Timing](parte-2-analisis-http/capturas/cap-analisis1-04.png)

### Evidencias — Análisis 2: GET a API REST (200 vs 404)
![Análisis 2 - Respuesta JSON](parte-2-analisis-http/capturas/cap-analisis2-01.png)
![Análisis 2 - Headers 200](parte-2-analisis-http/capturas/cap-analisis2-02.png)
![Análisis 2 - Detalle 1](parte-2-analisis-http/capturas/cap-analisis2-03.png)
![Análisis 2 - Detalle 2](parte-2-analisis-http/capturas/cap-analisis2-04.png)
![Análisis 2 - Detalle 3](parte-2-analisis-http/capturas/cap-analisis2-05.png)
![Análisis 2 - Detalle 4](parte-2-analisis-http/capturas/cap-analisis2-06.png)
![Análisis 2 - Petición 404](parte-2-analisis-http/capturas/cap-analisis2-07.png)
![Análisis 2 - Detalle 404](parte-2-analisis-http/capturas/cap-analisis2-08.png)

### Evidencias — Análisis 3: POST con Postman
![Análisis 3 - Configuración y tests](parte-2-analisis-http/capturas/cap-analisis3-01.png)
![Análisis 3 - Body enviado](parte-2-analisis-http/capturas/cap-analisis3-02.png)
![Análisis 3 - Respuesta con id asignado](parte-2-analisis-http/capturas/cap-analisis3-03.png)

## Herramientas utilizadas
- VS Code, Git, GitHub
- Google Chrome + DevTools (panel Network, Elements, Console)
- Postman (petición POST con tests automatizados)

## Conclusiones
Este laboratorio permitió configurar un entorno de desarrollo web completo y, sobre esa base, comprender en la práctica cómo funciona el protocolo HTTP detrás de cualquier aplicación web. Analizar la petición a example.com evidenció el mecanismo de caché condicional (304 Not Modified, headers Etag e If-Modified-Since), mientras que las peticiones a la API REST de jsonplaceholder mostraron la diferencia central entre servir HTML para un navegador y servir JSON para ser consumido por código, además de cómo los códigos de estado (200, 404, 201) comunican el resultado de una operación independientemente del formato del cuerpo. Trabajar con Postman y sus tests automatizados reforzó la importancia de validar programáticamente el comportamiento de una API en lugar de depender solo de inspección manual. En conjunto, este laboratorio conecta la configuración práctica del entorno de desarrollo con una comprensión más profunda del ciclo de vida de una petición HTTP, habilidad fundamental para depurar aplicaciones y consumir APIs en el resto del curso.