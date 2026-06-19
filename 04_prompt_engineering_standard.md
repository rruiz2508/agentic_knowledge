# Prompt Engineering Standard

## 1. Objetivo

Definir un estándar para crear prompts claros, robustos, mantenibles y seguros para agentes, assistants, GPTs personalizados, Copilot, Roo Code, DeepSeek y herramientas similares.

## 2. Principios

Un buen prompt debe ser:

- Claro.
- Específico.
- Mantenible.
- Reutilizable.
- Auditable.
- Seguro.
- Orientado a resultados.
- Con límites explícitos.
- Con formato de salida definido.
- Con criterios de aceptación.

## 3. Estructura recomendada

```text
# Rol

[Eres...]

# Contexto

[Información del usuario, proyecto, stack, restricciones.]

# Objetivo

[Qué debe lograr.]

# Alcance

[Qué incluye.]

# Fuera de alcance

[Qué no debe hacer.]

# Instrucciones

[Reglas operativas.]

# Herramientas disponibles

[Tools, permisos y restricciones.]

# Flujo de trabajo

[Pasos esperados.]

# Formato de salida

[Markdown, JSON, YAML, tabla, código, etc.]

# Guardrails

[Seguridad, límites, confirmaciones.]

# Criterios de aceptación

[Cómo saber si la respuesta es buena.]
```

## 4. Componentes principales

### Rol

Debe indicar la especialidad del agente.

Ejemplo:

```text
Eres un arquitecto de software especializado en sistemas empresariales .NET, SQL Server, SAP B1 y programación agéntica.
```

### Contexto

Debe incluir datos relevantes:

- Stack técnico.
- Tipo de proyecto.
- Restricciones.
- Herramientas.
- Público objetivo.
- Nivel de criticidad.
- Estado actual.

### Objetivo

Debe explicar el resultado esperado.

Ejemplo:

```text
Diseñar un agente que revise Pull Requests de proyectos .NET y genere observaciones técnicas accionables.
```

### Alcance

Debe definir qué puede hacer.

### Fuera de alcance

Debe definir qué no debe hacer.

### Instrucciones

Deben estar escritas como reglas concretas.

Ejemplo:

```text
Cuando detectes un problema, clasifícalo como crítico, importante o sugerencia.
```

### Formato de salida

Debe indicar claramente la estructura.

Ejemplo:

```markdown
## Resumen
## Hallazgos críticos
## Hallazgos importantes
## Sugerencias
## Próximos pasos
```

## 5. Prompt para agentes de desarrollo

```text
Eres un agente de desarrollo especializado en [stack].

Objetivo:
Implementar [funcionalidad] respetando la arquitectura existente.

Contexto:
- Proyecto: [nombre]
- Stack: [stack]
- Restricciones: [restricciones]
- Archivos relevantes: [archivos]

Reglas:
- No modifiques archivos fuera del alcance indicado.
- No elimines código existente sin justificarlo.
- Mantén compatibilidad con la arquitectura actual.
- Si hay dudas, documenta supuestos.
- Ejecuta pruebas si están disponibles.
- Reporta archivos modificados.

Salida:
1. Resumen de cambios.
2. Archivos modificados.
3. Pruebas ejecutadas.
4. Riesgos o pendientes.
```

## 6. Prompt para revisión de arquitectura

```text
Eres un arquitecto de software senior.

Analiza la siguiente propuesta técnica considerando:
- Mantenibilidad.
- Escalabilidad.
- Seguridad.
- Complejidad.
- Costos.
- Riesgos operativos.
- Compatibilidad con el stack existente.
- Impacto en equipos de desarrollo.
- Observabilidad.
- Estrategia de migración.

Entrega la respuesta en este formato:
1. Resumen ejecutivo.
2. Fortalezas.
3. Riesgos.
4. Preguntas abiertas.
5. Recomendaciones.
6. Decisión sugerida.
```

## 7. Prompt para documentación técnica

```text
Eres un redactor técnico especializado en documentación de software empresarial.

Objetivo:
Crear documentación clara, profesional y reutilizable sobre [tema].

Audiencia:
[Arquitectos / desarrolladores / analistas / proveedores / negocio]

Formato:
Markdown con títulos, tablas y ejemplos.

Debe incluir:
- Propósito.
- Alcance.
- Contexto.
- Diseño propuesto.
- Flujo.
- Consideraciones técnicas.
- Riesgos.
- Criterios de aceptación.
- Próximos pasos.
```

## 8. Prompt para diseño de agente

```text
Eres un consultor experto en programación agéntica.

Diseña un agente para [objetivo].

Debes incluir:
1. Nombre del agente.
2. Propósito.
3. Problema que resuelve.
4. Usuarios objetivo.
5. Alcance.
6. Fuera de alcance.
7. Nivel de autonomía.
8. Responsabilidades.
9. Entradas.
10. Salidas.
11. Tools.
12. Memoria.
13. Fuentes de conocimiento.
14. Flujo de trabajo.
15. Reglas de decisión.
16. Manejo de errores.
17. Guardrails.
18. Seguridad.
19. Observabilidad.
20. Costos.
21. Criterios de aceptación.
22. Ejemplos.
23. Prompt final del agente.
24. Configuración técnica sugerida.
25. Próximos pasos.
```

## 9. Anti-patrones

Evitar:

- Prompts demasiado vagos.
- Prompts sin alcance.
- Prompts sin formato de salida.
- Prompts que mezclan muchas responsabilidades.
- Prompts que permiten acciones destructivas sin confirmación.
- Prompts que no definen errores.
- Prompts que no explican criterios de éxito.
- Prompts que dependen de información no provista.
- Prompts que ocultan incertidumbre.
- Prompts que piden “hacer lo mejor posible” sin contexto.

## 10. Checklist de calidad

Antes de usar un prompt, validar:

- [ ] Tiene rol claro.
- [ ] Tiene objetivo claro.
- [ ] Tiene contexto suficiente.
- [ ] Tiene alcance.
- [ ] Tiene fuera de alcance.
- [ ] Tiene reglas operativas.
- [ ] Tiene formato de salida.
- [ ] Tiene guardrails.
- [ ] Tiene criterios de aceptación.
- [ ] No contiene contradicciones.
- [ ] No habilita acciones inseguras.
- [ ] Es mantenible y versionable.

## 11. Versionado

Todo prompt importante debería tener:

```yaml
prompt:
  name: ""
  version: "0.1.0"
  owner: ""
  status: "draft"
  last_updated: ""
  changelog:
    - version: "0.1.0"
      changes:
        - "Versión inicial"
```

## 12. Recomendación

Todo prompt de agente debe tratarse como un artefacto de software: versionado, revisado, probado y documentado.
