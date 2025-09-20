# Descripción de la Arquitectura de Software
 Este repositorio contiene la documentación de la arquitectura del sistema...
 ## Objetivo
 Aprender a trabajar con documentación técnica usando un flujo *docs-as-code*:- Texto plano con **AsciiDoc + Asciidoctor**.
- Control de versiones con **Git/GitHub o GitLab**.- Publicación automática de HTML y PDF con **CI/CD**.- Inclusión de diagramas creados en **Enterprise Architect**.
 ## Estructura del proyecto
 docs/
→ Documentación en AsciiDoc
 images/
build/
→ Diagramas exportados desde EA
 → Salida generada (ignorada en Git)
 ## Requisitos- Ruby (con Asciidoctor y Asciidoctor PDF instalados).- VS Code con el plugin [AsciiDoc by Asciidoctor].
 ## Compilación local (bash)
 asciidoctor -D build docs/index.adoc
 asciidoctor-pdf -o build/index.pdf docs/index.adoc
