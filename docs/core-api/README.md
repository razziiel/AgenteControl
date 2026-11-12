# Documentación del Agent Core (Espacio de Integración Backend ↔ UI)

Esta carpeta está destinada a alojar toda la documentación técnica, esquemas y ejemplos de la **API del Agent Core** para que podamos conectar `AgenteControl` (el frontend / Sistema Operativo Web) sin fricciones y pulir juntos el plan completo.

---

## Checklist de Información Necesaria del Core

Podés subir aquí archivos Markdown (`.md`), especificaciones OpenAPI/Swagger (`.json` / `.yaml`), diagramas o ejemplos de payloads cubriendo estos 5 puntos clave:

### 1. Arquitectura General y Ejecución
* ¿En qué lenguaje/framework está construido el Core y cómo se levanta localmente (Docker, Node, Python, binario, etc.)?
* ¿Cómo maneja la autenticación o separación por **Usuario**?

### 2. Proyectos, Subproyectos y Sistema de Archivos (Filesystem)
* ¿Cómo estructura hoy el Core los directorios de trabajo (workspaces) en disco?
* ¿Existen ya endpoints (o hay que definirlos) para:
  * Listar/crear **Proyectos** y **Subproyectos**.
  * Listar árbol de archivos, leer contenido, subir archivos (PDF, CSV, imágenes) y descargar archivos generados por los agentes.
  * Recibir notificaciones/eventos cuando un agente crea o modifica un archivo en vivo.

### 3. Agentes, Subagentes y Skills / Tools
* ¿Cómo se definen los **Agentes** y **Subagentes** (archivos de configuración, JSON, Markdown, base de datos)?
* ¿Qué formato tienen los **Skills** y las **Tools** en el Core?
* ¿Cómo podemos consultar desde la UI el catálogo de *skills* disponibles para asignarlos/habilitarlos en un proyecto o agente específico?

### 4. Protocolo de Comunicación en Tiempo Real (Streaming)
* ¿Cómo se envía una tarea o acción a un agente (`REST POST`, `WebSocket`, `SSE`, `gRPC`)?
* ¿Qué eventos emite el Core mientras trabaja? Por ejemplo:
  * Chunks de texto / razonamiento.
  * Inicio, argumentos y resultado de cada `Tool Call`.
  * Creación y estado de **Subagentes** hijos.
  * Solicitudes de confirmación (*Human-in-the-loop*) antes de ejecutar una acción sensible (ej. emitir factura en ARCA).

### 5. Gestión de Modelos y Consumo de Tokens
* ¿Cómo recibe o configura el Core las API keys / proveedores (`Anthropic`, `OpenAI`, modelos locales)?
* ¿Reporta métricas de consumo de tokens por ejecución/proyecto para mostrarlas en el panel de control?

---

## Cómo Subir tu Documentación

1. Cloná el repositorio:
   ```bash
   git clone https://github.com/razziiel/AgenteControl.git
   ```
2. Agregá tus archivos `.md`, diagramas o specs dentro de esta carpeta (`docs/core-api/`).
3. Hacé commit y push (o abrí un Pull Request) para unificar el contrato `packages/core-sdk` y arrancar con la interfaz del Sistema Operativo.
