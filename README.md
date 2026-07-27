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

**[Download the Archived Workflow Cleanup template](./Archived%20Workflow%20Cleanup.json)**

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

**[Descargar el template Archived Workflow Cleanup](./Archived%20Workflow%20Cleanup.json)**

## Sígueme en mis redes sociales

Sígueme para encontrar contenido práctico sobre automatizaciones, n8n y desarrollo con IA. Comparto técnicas, aprendizajes y detalles de uso real de los que casi nadie habla, pero que marcan la diferencia al construir soluciones que realmente funcionan.

- [TikTok](https://www.tiktok.com/@vibecodeandflow)
- [Instagram](https://www.instagram.com/vibecodeandflow/)
- [Facebook](https://www.facebook.com/vibecodeandflow/)
- [YouTube](https://www.youtube.com/@vibecodeandflow)
- [Creador Oficial de n8n](https://n8n.io/creators/junforever/)
- [Npmjs Org](https://npmjs.com/~junforever)
