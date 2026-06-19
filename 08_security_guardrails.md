# Security Guardrails

## 1. Objetivo

Definir guardrails de seguridad para agentes IA, tools, skills, prompts, automatizaciones y flujos agénticos.

## 2. Principios de seguridad

- Mínimo privilegio.
- Defensa en profundidad.
- Validación humana para acciones críticas.
- Trazabilidad.
- Protección de secretos.
- Separación de ambientes.
- Control de costos.
- Control de herramientas.
- Salidas estructuradas.
- Registro seguro.
- No confiar ciegamente en respuestas del modelo.

## 3. Clasificación de riesgo

| Nivel | Descripción | Ejemplo | Requiere aprobación |
|---|---|---|---|
| Bajo | Solo lectura, bajo impacto | Resumir documentación | No |
| Medio | Cambios locales o propuestas | Modificar archivo no crítico | Según caso |
| Alto | Cambios en repositorios o datos | Crear PR, ejecutar script | Sí |
| Crítico | Producción, datos sensibles, finanzas | Modificar BD productiva | Sí, formal |

## 4. Acciones que siempre requieren aprobación humana

- Borrar archivos.
- Modificar archivos críticos.
- Ejecutar comandos de shell.
- Instalar paquetes.
- Ejecutar scripts SQL.
- Modificar bases de datos.
- Llamar APIs de escritura.
- Enviar correos.
- Crear, aprobar o fusionar PRs.
- Cambiar configuraciones de CI/CD.
- Modificar secretos.
- Realizar despliegues.
- Acceder a datos sensibles.
- Cambiar permisos.

## 5. Acciones prohibidas por defecto

- Exponer secretos.
- Imprimir tokens.
- Registrar contraseñas.
- Ejecutar comandos destructivos sin confirmación.
- Modificar producción sin autorización.
- Desactivar seguridad.
- Saltar validaciones.
- Crear backdoors.
- Ejecutar código no confiable.
- Consultar datos personales sin motivo válido.
- Generar SQL libre contra producción.

## 6. Protección de secretos

Nunca incluir en prompts, logs o documentación:

- API keys.
- Passwords.
- Tokens.
- Refresh tokens.
- Private keys.
- Connection strings.
- Cookies.
- Credenciales de SAP.
- Credenciales de bases de datos.
- Archivos `.env`.
- Certificados.

Usar placeholders:

```text
{{API_KEY}}
{{DB_CONNECTION_STRING}}
{{SAP_USERNAME}}
{{SAP_PASSWORD}}
```

## 7. Control de tools

Toda tool debe documentar:

| Campo | Descripción |
|---|---|
| Nombre | Identificador de la tool. |
| Propósito | Para qué sirve. |
| Parámetros | Entradas permitidas. |
| Permisos | Lectura, escritura, ejecución. |
| Riesgo | Bajo, medio, alto, crítico. |
| Aprobación | Si requiere confirmación humana. |
| Logs | Qué se registra. |
| Restricciones | Límites explícitos. |

## 8. Guardrails para archivos

- Limitar escritura a carpetas permitidas.
- No modificar `.git`, `.env`, certificados ni secretos.
- Crear backup antes de cambios masivos.
- Mostrar diff antes de aplicar cambios críticos.
- No borrar sin confirmación.
- Evitar cambios fuera del alcance.
- Documentar archivos modificados.

## 9. Guardrails para shell

Antes de ejecutar comandos:

- Explicar propósito.
- Mostrar comando.
- Indicar impacto.
- Confirmar si es destructivo.
- Evitar comandos con `rm -rf`, `del /s`, `format`, `drop`, `truncate`.
- Evitar comandos descargados de internet sin revisión.
- Usar ambientes aislados cuando sea posible.

## 10. Guardrails para bases de datos

- No ejecutar SQL generado por IA directamente en producción.
- Usar cuentas de solo lectura cuando sea posible.
- Prohibir `DROP`, `TRUNCATE`, `DELETE` y `UPDATE` sin aprobación formal.
- Usar transacciones.
- Hacer backup.
- Validar `WHERE`.
- Limitar resultados.
- Evitar datos personales innecesarios.
- Registrar queries ejecutadas.
- Probar primero en ambiente de desarrollo.

## 11. Guardrails para SAP B1

- No modificar objetos de negocio sin validación.
- Usar entornos de prueba.
- Validar permisos.
- Registrar errores.
- Controlar transacciones.
- No exponer credenciales.
- Validar impacto contable, comercial o financiero.
- Requerir aprobación para operaciones de escritura.

## 12. Guardrails para repositorios

- Crear rama separada.
- No pushear directo a `main`.
- No modificar pipelines sin revisión.
- No modificar permisos.
- No alterar historial Git sin aprobación.
- Crear PR para revisión.
- Ejecutar pruebas.
- Documentar cambios.

## 13. Guardrails para prompts

- No incluir secretos.
- No incluir datos personales innecesarios.
- No dar instrucciones contradictorias.
- Definir límites.
- Definir formato de salida.
- Definir cuándo escalar a humano.
- Definir acciones prohibidas.
- Versionar prompts críticos.

## 14. Guardrails para memoria

- No guardar secretos.
- No guardar datos sensibles sin necesidad.
- Definir retención.
- Permitir corrección de información obsoleta.
- Separar memoria de usuario, proyecto y ejecución.
- Registrar fuente de información.
- Evitar usar memoria antigua sin validarla.

## 15. Guardrails para costos

- Definir modelo por defecto.
- Limitar iteraciones.
- Limitar tamaño de contexto.
- Evitar loops infinitos.
- Registrar tokens.
- Estimar costo por ejecución.
- Usar modelos económicos para tareas repetitivas.
- Reservar modelos avanzados para diseño, revisión y decisiones complejas.

## 16. Guardrails para respuestas

El agente debe:

- Declarar supuestos.
- Declarar incertidumbre.
- No inventar fuentes.
- No ocultar riesgos.
- No presentar acciones inseguras como seguras.
- Indicar cuándo se requiere validación.
- Dar alternativas de menor riesgo.

## 17. Checklist de seguridad

- [ ] ¿La acción es de lectura o escritura?
- [ ] ¿Hay riesgo productivo?
- [ ] ¿Hay datos sensibles?
- [ ] ¿Hay secretos?
- [ ] ¿La tool tiene permisos mínimos?
- [ ] ¿Se necesita aprobación humana?
- [ ] ¿Existe rollback?
- [ ] ¿Se registrará la acción?
- [ ] ¿El costo está controlado?
- [ ] ¿La salida fue validada?
- [ ] ¿Se documentaron riesgos?

## 18. Política de aprobación

```yaml
approval_policy:
  file_write:
    required: true
    except_paths:
      - "docs/"
  shell_execution:
    required: true
  database_read:
    required: false
    conditions:
      - "readonly_user"
      - "non_sensitive_data"
  database_write:
    required: true
  production_access:
    required: true
  external_api_write:
    required: true
```

## 19. Recomendación

Todo agente con capacidad de actuar sobre archivos, comandos, bases de datos, repositorios o APIs debe diseñarse como sistema controlado, no como asistente libre. La autonomía debe ganarse gradualmente mediante pruebas, logs y revisión humana.
