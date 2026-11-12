# AgenteControl — Agent OS Web & Vertical Apps

`AgenteControl` es la capa visual estilo **Sistema Operativo Web (Control Plane + UI Generativa)** diseñada para conectarse vía API a un **Core de Agentes** externo con acceso a archivos, herramientas (*tools*), *skills* y ejecución de subagentes.

El objetivo del proyecto es separar limpiamente el **motor de ejecución agéntico (Core)** de las **aplicaciones web especializadas por nicho** que utiliza cada cliente final (100% Web App, sin depender de WhatsApp).

---

## Arquitectura de Dos Capas

| Capa | Responsabilidad | Repositorio / Ubicación |
| :--- | :--- | :--- |
| **1. Agent Core (Backend / Motor)** | Orquestación de agentes y subagentes, ejecución de *skills* y *tools*, acceso a sistema de archivos (*filesystem*), memoria y consumo/ruteo de LLMs. | Documentación de integración en [`docs/core-api/`](./docs/core-api/README.md) |
| **2. AgenteControl (Frontend / Web OS)** | Interfaz multi-usuario de **Proyectos y Subproyectos**, explorador/visor de archivos en tiempo real, árbol de agentes/subagentes activos y **Vistas Verticales por rubro**. | Este repositorio (`apps/` y `packages/`) |

---

## Jerarquía Universal del Sistema

Antes de cada aplicación vertical, `AgenteControl` administra una estructura común para cualquier usuario:

1. **Usuario / Cuenta**
2. **Proyectos y Subproyectos** (aislados a nivel de carpetas/archivos y contexto).
3. **Sistema de Archivos Integrado** (subida, edición y previsualización en vivo de PDFs, CSV/Excel, JSON, Markdown y reportes generados por los agentes).
4. **Equipo de Agentes y Subagentes** asignados al proyecto con su set específico de **Skills** habilitados.
5. **Vistas Especializadas (Apps de Nicho)** que disparan acciones contra el Core con 1 clic (sin obligar al cliente a redactar prompts técnicos).

---

## Primeras Aplicaciones Verticales Planificadas (Tucumán / Argentina)

1. **`market-radar` — Inteligencia de Precios Local y Mapa Visual por Zonas:** Relevamiento automatizado de precios (SEPA, cadenas regionales, mayoristas y e-commerce) renderizado en mapas de calor geoespaciales (`PostGIS` + `MapLibre` / `Deck.gl`) para supermercados, distribuidoras y comercios.
2. **`contadores-ar` — Suite Web para Estudios Contables:** Gestión por cliente/CUIT como subproyecto, consultas y acciones directas ante **ARCA (ex AFIP)** vía Web Services, lectura estructurada de comprobantes/extractos y papeles de trabajo para **DGR Tucumán (`SiAPre`)** y **TEM**.
3. **`legal-tuc` — Workstation para Abogados y Jurisprudencia Verificada:** Gestión de causas/expedientes (**SAE Tucumán**), buscador híbrido de legislación y jurisprudencia real (**CSJT / Cámaras de Tucumán / SAIJ / InfoLeg**) con citas 100% verificadas anti-alucinaciones y redacción asistida.

---

## Documentación del Proyecto

* **[`docs/ARQUITECTURA_Y_PLAN.md`](./docs/ARQUITECTURA_Y_PLAN.md):** Blueprint completo de arquitectura, stack open-source reutilizable para no empezar de cero, estrategia de ruteo de tokens y diseño de cada módulo vertical.
* **[`docs/core-api/README.md`](./docs/core-api/README.md):** Espacio dedicado para subir la documentación técnica del **Agent Core** (endpoints, eventos de streaming, manejo de archivos, formato de *skills* y subagentes) y definir el contrato entre ambos sistemas.

---

## Próximos Pasos (Workflow de Equipo)

1. **Subir documentación del Core** en [`docs/core-api/`](./docs/core-api/README.md) (arquitectura actual del bot, endpoints existentes o propuestos, estructura de carpetas/workspaces y definición de skills).
2. **Definir el Contrato UI ↔ Core** (REST + SSE/WebSockets / protocolo `AG-UI`).
3. **Inicializar el Monorepo (`pnpm` + `Next.js` + `TypeScript` + `Tailwind`)** construyendo primero el **Shell Base de `AgenteControl`** (Proyectos, Explorador de Archivos y Monitor de Agentes/Subagentes) antes de montar los módulos verticales.
