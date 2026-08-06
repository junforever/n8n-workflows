# Production-Ready n8n Workflows

This repository contains practical, high-quality n8n workflows designed for real-world use. These are more than isolated examples: each workflow addresses a concrete need and includes the logic, safeguards, and documentation required for realistic scenarios.

Every workflow includes instructions in both English and Spanish explaining how to configure it, run it, and understand how it works—so there is no language barrier and no excuse not to put it to use.

## Available Workflows

### Gitops Engine - Back Up n8n Workflows to GitHub

Backs up every non-archived n8n workflow as a readable JSON file in the root of a GitHub repository. It detects new, modified, renamed, and deleted workflows and keeps the repository synchronized accordingly.

For faster processing and reliable comparisons, each filename includes the workflow ID and a deterministic semantic SHA-256 generated from the workflow data that affects its behavior: `nodes`, `connections`, and `settings`. The workflow can therefore compare the metadata encoded in filenames instead of downloading every existing JSON file from GitHub on each run. This reduces API requests, data transfer, memory usage, and execution time while producing accurate change detection for the selected properties.

**[GitOps Engine workflow official n8n page template](https://n8n.io/workflows/17352)**

### GitOps Restore Engine - Restore n8n Workflows from GitHub

Restores n8n workflows from the JSON backups created by GitOps Engine and stored in the root of a GitHub repository. It cleans unsupported workflow settings before creation and uses an n8n Data Table as a temporary checkpoint, allowing an interrupted restoration to continue without processing completed backups again.

Workflow files are downloaded through GitHub's raw content API because the standard Contents API does not include the `content` field for files larger than 1 MB. This allows GitOps Restore Engine to handle larger workflow backups without depending on the Base64 content returned by GitHub's native **Get file** operation.

**[GitOps Restore Engine workflow official n8n page template](https://n8n.io/workflows/17388)**

### Archived Workflow Cleanup - Safely Delete Old Archived Workflows

Safely previews and deletes archived n8n workflows older than a configurable retention period. It filters out non-archived workflows before classification and separates archived workflows into three exclusive groups: deletion candidates, workflows retained because they are still within the retention period, and workflows protected by a configurable tag.

The workflow starts in `dry_run` mode, requires a `project_id` before live deletion, and processes deletions in configurable batches. Its final summary reports the archived total, candidates, protected workflows, retained workflows, successful deletions, and failures. Deletion is permanent and also removes the deleted workflow's execution history.

**[Archived Cleanup workflow official n8n page template](https://n8n.io/workflows/17533)**

## Additional Resources

### n8n-library - Quick Local Setup (Docker)

[n8n-library](https://github.com/LPilic/n8n-library) is an open-source, self-hosted companion application designed to extend and centralize the management of your [n8n](https://n8n.io) ecosystem.

Although **the project is currently under active construction**, its available feature set already provides everything needed to perform powerful, effective monitoring and management across your n8n instances.

#### Key Features & Highlights:

- **Monitoring & Observability Dashboard**: Track execution statistics in real-time, inspect node-level timelines, activate/deactivate workflows, and monitor system performance (CPU, memory, queues, and worker health).
- **Multi-Instance Support**: Easily monitor and switch between multiple n8n instances (e.g., Production, Staging, Dev) from a single unified interface.
- **Template Library**: Browse, search, and import workflow templates directly into your n8n instances.
- **Service Desk & Knowledge Base**: Manage internal incident tickets linked directly to n8n workflow executions, alongside a searchable documentation base.
- **AI Assistant & MCP Integration**: Built-in chat powered by LLMs (Claude, OpenAI, Gemini, Groq, Ollama) with Model Context Protocol (MCP) support (such as `n8n-mcp`) to manage workflows via conversation.
- **Role-Based Access & API Keys**: Granular permissions (Admin, Editor, Viewer) and API key generation for programmatic access.

---

The `n8n-library/` folder contains all the necessary files (`Dockerfile`, `docker-compose.yml`, and `.env`) ready to copy and paste directly into the root of the `n8n-library` project, allowing you to run it locally with Docker right away without having to change anything.

#### Default Access Credentials:

- **Email:** `admin@localhost`
- **Password:** `admin`

#### How to use:

1. Clone or download the official [n8n-library](https://github.com/LPilic/n8n-library) repository.
2. Copy the three files from the `n8n-library/` folder in this repo into the root of your cloned `n8n-library` project.
3. Run the following command in your terminal:
   ```bash
   docker compose up -d
   ```
4. Access the application in your browser at `http://localhost:3100/`.
5. Log in using the default access credentials.
6. Once inside, navigate to the `Admin` section in the left sidebar menu and select `Settings`.
7. Inside the `Settings` section, click the `Add Instance` button.
8. In the modal that appears, enter the following information:
   - `Name`: Instance name
   - `Environment`: Specify whether it is for development, staging, production, etc.
   - `Internal URL`: The URL of your n8n instance (local or hosted on a VPS).
   - `API Key`: API Key for your n8n instance (you must generate it in your n8n instance under `Settings` -> `n8n API` -> `Create API Key`).
9. Click `Save`.
10. Done! Now go to the `Main` section, select `Dashboard`, and your instance should appear as `Healthy`.

> [!WARNING]
> **Environment Variables & Production Deployment Notice:**
>
> - The included `.env` file contains default values intended strictly for **local testing**. **DO NOT USE THESE VALUES ON A VPS OR IN PRODUCTION.**
> - Default credentials (`admin@localhost` / `admin`) **must be changed immediately for production deployments**.
> - To generate a secure `SESSION_SECRET` value in the Windows console, run:
>   ```powershell
>   openssl rand -hex 32
>   ```
>   _(If `openssl` is not recognized, install it with `winget install openssl`)_

## Follow me on my social networks

Follow me for practical content about automation, n8n, and AI development. I share real-world techniques, lessons, and details that almost nobody talks about—but that make a real difference when building solutions that actually work.

- [TikTok](https://www.tiktok.com/@vibecodeandflow)
- [Instagram](https://www.instagram.com/vibecodeandflow/)
- [Facebook](https://www.facebook.com/vibecodeandflow/)
- [YouTube](https://www.youtube.com/@vibecodeandflow)
- [n8n Official Creator](https://n8n.io/creators/junforever/)
- [Npmjs Org](https://npmjs.com/~junforever)

---

# Workflows de n8n listos para producción

Este repositorio contiene workflows de n8n prácticos y de alta calidad, diseñados para usarse en situaciones reales. Son más que ejemplos aislados: cada workflow resuelve una necesidad concreta e incluye la lógica, las medidas de seguridad y la documentación necesarias para escenarios realistas.

Cada workflow incluye instrucciones en inglés y español para configurarlo, ejecutarlo y entender cómo funciona, así que no hay barreras de idioma ni pretextos para no aprovecharlo.

## Workflows disponibles

### Gitops Engine - Respaldo de workflows de n8n en GitHub

Respalda cada workflow no archivado de n8n como un archivo JSON legible en la raíz de un repositorio de GitHub. Detecta workflows nuevos, modificados, renombrados y eliminados, y mantiene el repositorio sincronizado según corresponda.

Para lograr un procesamiento más rápido y comparaciones confiables, cada nombre de archivo incluye el ID del workflow y un SHA-256 semántico determinista generado a partir de los datos que afectan su comportamiento: `nodes`, `connections` y `settings`. De esta manera, el workflow puede comparar los metadatos incluidos en los nombres sin descargar desde GitHub todos los archivos JSON existentes en cada ejecución. Esto reduce las peticiones a la API, la transferencia de datos, el uso de memoria y el tiempo de ejecución, mientras detecta con precisión los cambios en las propiedades seleccionadas.

**[Página oficial del template GitOps Engine en n8n](https://n8n.io/workflows/17352)**

### GitOps Restore Engine - Restauración de workflows de n8n desde GitHub

Restaura workflows de n8n a partir de los respaldos JSON creados por GitOps Engine y almacenados en la raíz de un repositorio de GitHub. Antes de crear cada workflow, elimina los settings no admitidos y utiliza una Data Table de n8n como checkpoint temporal, lo que permite continuar una restauración interrumpida sin volver a procesar los respaldos completados.

Los archivos se descargan mediante el API de contenido raw de GitHub porque el Contents API estándar no incluye el campo `content` para archivos de más de 1 MB. Esto permite que GitOps Restore Engine procese respaldos de mayor tamaño sin depender del contenido Base64 devuelto por la operación nativa **Get file** de GitHub.

**[Página oficial del template GitOps Restore Engine en n8n](https://n8n.io/workflows/17388)**

### Archived Workflow Cleanup - Eliminación segura de workflows archivados antiguos

Previsualiza y elimina de forma segura workflows archivados de n8n que superen un periodo de retención configurable. Descarta los workflows no archivados antes de clasificarlos y divide los archivados en tres grupos exclusivos: candidatos para eliminación, workflows conservados porque todavía están dentro del periodo de retención y workflows protegidos mediante una etiqueta configurable.

El workflow comienza en modo `dry_run`, exige un `project_id` antes de habilitar la eliminación real y procesa los borrados en lotes configurables. Su resumen final informa el total de archivados, candidatos, workflows protegidos, workflows conservados, eliminaciones exitosas y errores. La eliminación es permanente y también borra el historial de ejecuciones del workflow eliminado.

**[Página oficial del template Archived Cleanup en n8n](https://n8n.io/workflows/17533)**

## Recursos adicionales

### n8n-library - Configuración rápida en local (Docker)

[n8n-library](https://github.com/LPilic/n8n-library) es una aplicación complementaria (_companion app_) de código abierto y autoalojada (_self-hosted_), diseñada para centralizar y potenciar la gestión de tu ecosistema de [n8n](https://n8n.io).

Aunque **el proyecto se encuentra actualmente en construcción**, las funcionalidades que ya tiene listas ofrecen todo lo necesario para realizar un monitoreo continuo, preciso y altamente efectivo de tus flujos e instancias de n8n.

#### Funcionalidades destacadas:

- **Dashboard de Monitoreo y Observabilidad**: Visualiza estadísticas de ejecución en tiempo real, inspecciona detalles a nivel de nodos, activa o desactiva flujos y monitorea el rendimiento del sistema (CPU, memoria, colas de ejecución y salud de workers).
- **Soporte Multi-Instancia**: Monitorea y alterna fácilmente entre múltiples entornos de n8n (ej. Producción, Staging, Desarrollo) desde un único panel centralizado.
- **Biblioteca de Templates**: Explora, busca e importa plantillas de workflows directamente hacia tus instancias de n8n.
- **Service Desk y Base de Conocimientos**: Sistema de tickets para soporte enlazado a ejecuciones específicas de n8n y gestión de artículos de documentación interna.
- **Asistente IA e Integración MCP**: Chat integrado impulsado por LLMs (Claude, OpenAI, Gemini, Groq, Ollama) con soporte para servidores Model Context Protocol (como `n8n-mcp`) para administrar flujos mediante conversación.
- **Control de Acceso (RBAC) y API Keys**: Roles de usuario (Admin, Editor, Viewer) con permisos granulares y generación de API keys para acceso programático.

---

El contenido de la carpeta `n8n-library/` incluye los archivos necesarios (`Dockerfile`, `docker-compose.yml` y `.env`) listos para copiar y pegar directamente en la raíz de tu proyecto `n8n-library` y poder ejecutarlo en local mediante Docker sin tener que modificar nada.

#### Credenciales de acceso por defecto:

- **Email:** `admin@localhost`
- **Password:** `admin`

#### Cómo usarlo:

1. Clona o descarga el proyecto oficial de [n8n-library](https://github.com/LPilic/n8n-library).
2. Copia los tres archivos de la carpeta `n8n-library/` de este repositorio a la raíz de tu proyecto `n8n-library` local.
3. Ejecuta el siguiente comando en la consola:
   ```bash
   docker compose up -d
   ```
4. Accede a la aplicación desde tu navegador en `http://localhost:3100/`.
5. Ingresa las credenciales de acceso por defecto.
6. Una vez dentro, en el menú lateral izquierdo ve a la sección `Admin` y selecciona la opción `Settings`.
7. Dentro de la sección `Settings`, clic en el botón `Add Instance`.
8. En el modal que aparece, ingresa la siguiente información:
   - `Name`: Nombre de la instancia
   - `Environment`: Especifica si es para desarrollo, staging, producción, etc.
   - `Internal URL`: La url de la instancia (local o en una VPS) de n8n.
   - `API Key`: API Key de la instancia de n8n (debes crearla en la configuración de tu instancia de n8n, menú `Settings` -> `n8n API` -> `Create API Key`).
9. Clic en Save.
10. ¡Listo! Ahora ve a la sección `Main` opción `Dashboard` y tu instancia debe aparecer como `Healthy`.

> [!WARNING]
> **Variables de entorno y aviso de seguridad:**
>
> - El archivo `.env` en la carpeta contiene valores por defecto pensados netamente para **pruebas en local**. **NO DEBEN USARSE ESOS VALORES PARA UN DESPLIEGUE EN UNA VPS O PRODUCCIÓN.**
> - De igual forma, las credenciales por defecto (`admin@localhost` / `admin`) **deben ser cambiadas obligatoriamente para producción**.
> - Para generar el valor de la variable de entorno `SESSION_SECRET` en la consola de Windows, ejecuta:
>   ```powershell
>   openssl rand -hex 32
>   ```
>   _(Si te sale que `openssl` no es reconocido, instálalo con `winget install openssl`)_

## Sígueme en mis redes sociales

Sígueme para encontrar contenido práctico sobre automatizaciones, n8n y desarrollo con IA. Comparto técnicas, aprendizajes y detalles de uso real de los que casi nadie habla, pero que marcan la diferencia al construir soluciones que realmente funcionan.

- [TikTok](https://www.tiktok.com/@vibecodeandflow)
- [Instagram](https://www.instagram.com/vibecodeandflow/)
- [Facebook](https://www.facebook.com/vibecodeandflow/)
- [YouTube](https://www.youtube.com/@vibecodeandflow)
- [Creador Oficial de n8n](https://n8n.io/creators/junforever/)
- [Npmjs Org](https://npmjs.com/~junforever)
