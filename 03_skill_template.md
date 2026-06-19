# Skill Template

## 1. Nombre de la skill

```text
[Nombre claro y específico]
```

## 2. Objetivo

Describir qué capacidad agrega esta skill al agente.

Ejemplo:

> Esta skill permite analizar un archivo Markdown de documentación técnica y proponer mejoras de estructura, claridad, completitud y consistencia.

## 3. Cuándo usar esta skill

Usar cuando:

- 
- 
- 

## 4. Cuándo no usar esta skill

No usar cuando:

- La tarea requiere permisos no disponibles.
- La tarea implica acciones destructivas sin aprobación.
- No existe suficiente contexto.
- La tarea pertenece a otra skill más específica.
- El usuario solicita algo fuera del alcance definido.

## 5. Entradas requeridas

| Entrada | Tipo | Obligatoria | Ejemplo | Descripción |
|---|---|---:|---|---|
| Instrucción | Texto | Sí | "Revisa este prompt" | Solicitud principal del usuario. |
| Contexto | Texto / Archivo | No | `README.md` | Información adicional para ejecutar la skill. |
| Restricciones | Texto | No | "No modificar formato" | Límites o condiciones. |

## 6. Salidas esperadas

| Salida | Tipo | Ejemplo |
|---|---|---|
| Resultado principal | Markdown | Diseño, análisis, prompt o configuración. |
| Observaciones | Lista | Riesgos, mejoras, advertencias. |
| Próximos pasos | Lista | Acciones recomendadas. |

## 7. Dependencias

- Modelo de lenguaje.
- Herramientas disponibles.
- Archivos de contexto.
- Documentación oficial, si aplica.
- Permisos de lectura o escritura, si aplica.

## 8. Procedimiento

1. Entender la intención del usuario.
2. Identificar si la skill aplica.
3. Revisar entradas disponibles.
4. Detectar restricciones.
5. Aplicar el procedimiento específico.
6. Validar salida contra criterios de aceptación.
7. Informar riesgos o supuestos.
8. Entregar resultado en formato reutilizable.

## 9. Validaciones

Antes de responder:

- Confirmar que el resultado cumple el objetivo.
- Verificar que no se excede el alcance.
- Revisar si hay riesgos de seguridad.
- Revisar si se requiere aprobación humana.
- Revisar si hay datos sensibles.
- Revisar si la respuesta es accionable.
- Revisar si la salida está en el formato esperado.

## 10. Restricciones

- No asumir acceso a sistemas externos.
- No inventar datos.
- No ejecutar acciones destructivas.
- No exponer secretos.
- No generar configuraciones inseguras.
- No mezclar responsabilidades con otra skill sin indicarlo.
- No ocultar incertidumbre.

## 11. Errores comunes

| Error | Causa probable | Solución |
|---|---|---|
| Skill demasiado genérica | Objetivo poco definido | Acotar propósito. |
| Salida ambigua | Falta formato esperado | Definir estructura de salida. |
| Riesgo no identificado | Falta guardrails | Agregar validaciones. |
| Dependencia oculta | Se asumió una herramienta | Documentar dependencia. |
| Resultado no reutilizable | Falta plantilla | Entregar Markdown/YAML/JSON. |

## 12. Ejemplo de uso

### Entrada

```text
Crea una skill para revisar prompts de agentes antes de subirlos a producción.
```

### Salida esperada

```markdown
# Skill: Prompt Review

## Objetivo
Revisar prompts de agentes para detectar ambigüedad, riesgos, instrucciones contradictorias, falta de guardrails y problemas de mantenibilidad.

## Cuándo usarla
- Antes de publicar un agente.
- Antes de versionar instrucciones.
- Cuando un agente se comporte de forma inconsistente.
```

## 13. Implementación sugerida

```text
Eres una skill especializada en [objetivo].

Debes:
1. Revisar la entrada.
2. Identificar problemas.
3. Clasificarlos por severidad.
4. Proponer mejoras.
5. Entregar una versión corregida si aplica.

No debes:
- Inventar requisitos.
- Ocultar riesgos.
- Ejecutar acciones fuera de alcance.
```

## 14. Criterios de aceptación

- La skill tiene un objetivo claro.
- Indica cuándo usarla y cuándo no.
- Define entradas y salidas.
- Tiene restricciones explícitas.
- Incluye validaciones.
- Incluye ejemplos.
- Puede ser reutilizada por un agente.
