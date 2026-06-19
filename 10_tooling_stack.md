# Tooling Stack

## 1. Objetivo

Documentar el mapa de herramientas de IA y desarrollo utilizadas, separando claramente sus roles dentro del flujo de trabajo.

## 2. Principio rector

ChatGPT es el consultor estratégico y aliado para arquitectura, documentación, diseños y planes.

Las demás herramientas actúan como constructores, asistentes especializados o ejecutores.

## 3. Mapa de herramientas

| Herramienta | Rol principal | Uso recomendado |
|---|---|---|
| ChatGPT Plus | Consultor estratégico | Arquitectura, documentación, planes, diseño, análisis. |
| GPT personalizado Agentic Software Architect | Especialista en programación agéntica | Diseño de agentes, skills, prompts, workflows, guardrails. |
| GitHub Copilot Pro | Constructor dentro del IDE | Autocompletado, refactorización, generación de código, tests. |
| Roo Code | Agente ejecutor | Cambios multiarchivo, tareas largas, automatización. |
| DeepSeek API | Modelo económico para ejecución | Tareas extensas, generación masiva, agentes de bajo costo. |
| Gemini / Google AI Plus | Complemento de análisis y documentos | Documentos grandes, Drive, segunda opinión. |
| VS Code | Entorno principal liviano | Desarrollo, Copilot, Roo Code, edición. |
| Visual Studio | IDE fuerte para .NET | Proyectos .NET complejos, debugging, herramientas Microsoft. |
| GitHub | Repositorios y colaboración | PRs, issues, actions, versionado. |
| GitHub Actions | CI/CD | Build, test, despliegue, automatización. |

## 4. División ideal de trabajo

```text
ChatGPT / GPT personalizado
        ↓
Diseño, arquitectura, documentación, prompts, planes
        ↓
Copilot / Roo Code / DeepSeek
        ↓
Implementación, cambios de código, pruebas, automatización
        ↓
ChatGPT / GPT personalizado
        ↓
Revisión, validación, documentación final
```

## 5. ChatGPT Plus

Usar para:

- Arquitectura de sistemas.
- Diseño de soluciones.
- Reingeniería del CORE.
- Estrategias de integración SAP B1.
- Diseño de bases de datos.
- Documentación técnica.
- Planes de trabajo.
- Revisión de propuestas.
- Análisis de riesgos.
- Creación de estándares.
- Diseño de agentes y skills.

No usar principalmente para:

- Autocompletado continuo.
- Edición masiva de archivos dentro del IDE.
- Ejecución repetitiva de tareas largas si existe alternativa más económica.

## 6. GPT personalizado Agentic Software Architect

Usar para:

- Crear agentes.
- Documentar agentes.
- Diseñar skills.
- Revisar prompts.
- Crear AGENTS.md.
- Diseñar workflows LangGraph.
- Diseñar soluciones LangChain.
- Definir guardrails.
- Preparar configuraciones.
- Revisar herramientas agénticas.
- Convertir ideas en especificaciones técnicas.

## 7. GitHub Copilot Pro

Usar para:

- Autocompletado.
- Generar código repetitivo.
- Refactorizar.
- Explicar código.
- Crear tests.
- Trabajar en proyectos .NET.
- Revisar PRs.
- Corregir errores de compilación.
- Asistir dentro de VS Code.

Buenas prácticas:

- Mantener pocas extensiones.
- No aceptar cambios grandes sin revisión.
- Usar instrucciones de repositorio.
- Crear tareas pequeñas y claras.
- Revisar diffs.
- Ejecutar tests.

## 8. Roo Code + DeepSeek

Usar para:

- Tareas largas.
- Cambios multiarchivo.
- Generación masiva.
- Automatización de bajo costo.
- Refactorizaciones controladas.
- Creación de documentación desde código.
- Aplicación de plantillas.

Buenas prácticas:

- Trabajar en ramas separadas.
- Dar instrucciones muy específicas.
- Limitar alcance.
- Revisar cambios.
- No dar acceso irrestricto a secretos.
- Evitar acciones destructivas.

## 9. Gemini / Google AI Plus

Usar para:

- Documentos en Google Drive.
- Análisis alternativo.
- Segunda opinión.
- Archivos extensos.
- Trabajo con ecosistema Google.
- Resúmenes de documentos.
- Productividad general.

## 10. VS Code

Perfil recomendado para trabajo .NET + SQL Server + IA:

Extensiones base:

- C# Dev Kit.
- C#.
- .NET Install Tool.
- GitHub Pull Requests and Issues.
- GitLens.
- SQL Server / MSSQL.
- GitHub Copilot.
- Roo Code, si se usa.
- EditorConfig.
- Markdown All in One, opcional.

Evitar exceso de extensiones para mantener rendimiento.

## 11. Visual Studio

Usar cuando:

- El proyecto .NET requiera tooling avanzado.
- Se necesite debugging profundo.
- Se trabaje con soluciones grandes.
- Se requieran herramientas oficiales Microsoft no disponibles en VS Code.
- Se trabaje con Windows Forms, WPF o componentes legacy.

## 12. GitHub

Usar para:

- Repositorios.
- Pull Requests.
- Issues.
- Wiki o documentación.
- GitHub Actions.
- Gestión de ramas.
- Revisión de código.

Buenas prácticas:

- Ramas por tarea.
- PRs pequeños.
- Descripción clara.
- Checks automáticos.
- Revisión humana.
- Uso de `AGENTS.md` en repositorios con agentes.

## 13. Flujo recomendado para tareas de desarrollo

1. Diseñar solución con ChatGPT o GPT personalizado.
2. Convertir diseño en tareas pequeñas.
3. Crear rama de trabajo.
4. Usar Copilot o Roo Code para implementar.
5. Ejecutar pruebas.
6. Revisar diff.
7. Documentar cambios.
8. Crear PR.
9. Revisar con ChatGPT si hay decisiones complejas.
10. Fusionar tras validación.

## 14. Flujo recomendado para agentes

1. Definir propósito.
2. Definir alcance.
3. Definir nivel de autonomía.
4. Diseñar tools.
5. Diseñar memoria.
6. Definir guardrails.
7. Crear prompt.
8. Crear configuración.
9. Crear casos de prueba.
10. Ejecutar piloto.
11. Medir resultados.
12. Ajustar.
13. Documentar versión.

## 15. Decisiones de uso

| Necesidad | Herramienta recomendada |
|---|---|
| Pensar arquitectura | ChatGPT Plus |
| Crear agente | GPT personalizado |
| Escribir código en IDE | GitHub Copilot |
| Cambiar muchos archivos | Roo Code |
| Reducir costo de generación | DeepSeek |
| Analizar documentos Drive | Gemini |
| Revisar diseño técnico | ChatGPT Plus |
| Generar tests rápidos | Copilot |
| Documentar skill | GPT personalizado |
| Diseñar workflow LangGraph | GPT personalizado |

## 16. Riesgos

| Riesgo | Mitigación |
|---|---|
| Demasiadas herramientas | Definir rol claro para cada una. |
| Costos duplicados | Usar cada herramienta donde aporta más valor. |
| Cambios no revisados | Revisar diffs y ejecutar tests. |
| Exposición de secretos | Usar placeholders y vaults. |
| Dependencia excesiva | Mantener criterio técnico humano. |
| Contexto fragmentado | Documentar decisiones y estándares. |

## 17. Recomendación

Mantener a ChatGPT y al GPT personalizado como centro de pensamiento, diseño y validación. Usar Copilot, Roo Code, DeepSeek y Gemini como fuerza de construcción especializada según el contexto.
