# .NET Agentic Guidelines

## 1. Objetivo

Definir recomendaciones para integrar agentes IA, herramientas agénticas y automatización asistida en proyectos .NET, C#, SQL Server y sistemas empresariales.

## 2. Principios

- Mantener arquitectura limpia.
- Separar lógica de negocio de lógica IA.
- Evitar dependencia directa del proveedor de IA en el dominio.
- Diseñar interfaces claras.
- Registrar decisiones y resultados.
- Validar entradas y salidas.
- Controlar costos.
- Proteger secretos.
- Usar revisión humana en acciones críticas.
- Diseñar para pruebas.

## 3. Arquitectura recomendada

```text
/src
  /Application
    /Agentic
      IAgentService.cs
      IToolRegistry.cs
      IModelGateway.cs
      IAgentMemory.cs
  /Domain
  /Infrastructure
    /AI
      OpenAIModelGateway.cs
      DeepSeekModelGateway.cs
      ToolRegistry.cs
      AgentMemoryRepository.cs
  /Api
    /Controllers
      AgentController.cs
/tests
  /Application.Tests
  /Infrastructure.Tests
/docs
  agents.md
  agentic-architecture.md
```

## 4. Capas

| Capa | Responsabilidad |
|---|---|
| Domain | Reglas de negocio puras, sin IA. |
| Application | Casos de uso, orquestación, contratos. |
| Infrastructure | Implementaciones de modelos, tools, memoria, APIs. |
| API | Endpoints o interfaces de entrada. |
| Tests | Validación de comportamiento. |

## 5. Interfaces sugeridas

```csharp
public interface IModelGateway
{
    Task<ModelResponse> CompleteAsync(ModelRequest request, CancellationToken cancellationToken = default);
}
```

```csharp
public interface IAgentService
{
    Task<AgentResult> ExecuteAsync(AgentRequest request, CancellationToken cancellationToken = default);
}
```

```csharp
public interface ITool
{
    string Name { get; }
    string Description { get; }
    Task<ToolResult> ExecuteAsync(ToolRequest request, CancellationToken cancellationToken = default);
}
```

## 6. Separación de responsabilidades

Evitar que el agente:

- Acceda directamente a la base de datos sin capa de aplicación.
- Ejecute SQL arbitrario.
- Modifique datos productivos sin validaciones.
- Conozca detalles internos innecesarios.
- Mezcle lógica de negocio con prompt engineering.

## 7. Configuración

Usar configuración externa:

```json
{
  "Agentic": {
    "DefaultModel": "model-name",
    "MaxIterations": 5,
    "RequireHumanApprovalForWrites": true,
    "EnableTracing": true,
    "EnableMemory": false
  }
}
```

## 8. Secretos

Nunca guardar claves en:

- Código fuente.
- `appsettings.json` versionado.
- Prompts.
- Logs.
- Documentación pública.

Usar:

- Variables de entorno.
- Secret Manager en desarrollo.
- Vault corporativo.
- Azure Key Vault, si aplica.
- GitHub Secrets para CI/CD.

## 9. Tools en .NET

Cada tool debe tener:

- Nombre.
- Descripción.
- DTO de entrada.
- DTO de salida.
- Validaciones.
- Logs.
- Manejo de errores.
- Permisos.
- Tests.

Ejemplo:

```csharp
public sealed class SearchCustomerTool : ITool
{
    public string Name => "search_customer";
    public string Description => "Busca clientes por código, documento o nombre.";

    public async Task<ToolResult> ExecuteAsync(ToolRequest request, CancellationToken cancellationToken = default)
    {
        // Validar entrada
        // Ejecutar caso de uso
        // Devolver resultado estructurado
        throw new NotImplementedException();
    }
}
```

## 10. SQL Server

Buenas prácticas:

- No permitir SQL libre generado por IA contra producción.
- Usar stored procedures o queries predefinidas.
- Validar parámetros.
- Aplicar mínimo privilegio.
- Usar cuentas de solo lectura cuando sea posible.
- Limitar tiempo de ejecución.
- Registrar consultas.
- Evitar devolver datos sensibles innecesarios.

## 11. SAP Business One

Para integraciones con SAP B1:

- No permitir modificaciones directas sin validación.
- Preferir Service Layer o DI API según contexto.
- Documentar endpoints utilizados.
- Validar objetos de negocio.
- Registrar errores de SAP.
- Manejar transacciones cuidadosamente.
- Separar ambiente de pruebas y producción.
- No exponer credenciales en prompts o logs.

## 12. Logging

Registrar:

- AgentId.
- CorrelationId.
- Usuario.
- Caso de uso.
- Modelo utilizado.
- Tools invocadas.
- Duración.
- Estado.
- Errores.
- Resultado resumido.
- Aprobaciones humanas.

No registrar:

- Claves API.
- Contraseñas.
- Tokens.
- Datos personales sensibles.
- Cadenas de conexión.
- Respuestas completas si contienen datos sensibles.

## 13. Observabilidad

Métricas recomendadas:

- Cantidad de ejecuciones.
- Tasa de éxito.
- Tasa de error.
- Latencia promedio.
- Tokens consumidos.
- Costo estimado.
- Tools más usadas.
- Aprobaciones requeridas.
- Reintentos.
- Incidentes.

## 14. Testing

Pruebas mínimas:

- Unit tests de tools.
- Tests de validación de DTOs.
- Tests de prompts críticos.
- Tests de parsing de salida.
- Tests de manejo de errores.
- Tests de permisos.
- Tests de regresión con ejemplos reales.
- Tests de integración en ambiente controlado.

## 15. CI/CD

Pipeline recomendado:

```yaml
name: dotnet-agentic-ci

on:
  pull_request:
  push:
    branches:
      - main

jobs:
  build-test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.0.x'

      - name: Restore
        run: dotnet restore

      - name: Build
        run: dotnet build --no-restore --configuration Release

      - name: Test
        run: dotnet test --no-build --configuration Release
```

## 16. Documentación mínima

Todo agente en un proyecto .NET debe tener:

- Propósito.
- Alcance.
- Diagrama.
- Tools.
- Configuración.
- Riesgos.
- Guardrails.
- Logs.
- Métricas.
- Casos de prueba.
- Criterios de aceptación.

## 17. Checklist

- [ ] El dominio no depende directamente de IA.
- [ ] Existen interfaces para modelo y tools.
- [ ] Los secretos están protegidos.
- [ ] Hay límites de costo e iteraciones.
- [ ] Hay logs seguros.
- [ ] Hay pruebas.
- [ ] Hay aprobación humana para acciones críticas.
- [ ] Hay documentación.
- [ ] Hay rollback o mitigación.
- [ ] Hay ambiente de prueba.

## 18. Recomendación

En sistemas empresariales .NET, tratar la IA como una capacidad de aplicación, no como el centro del dominio. El agente debe integrarse mediante contratos claros, permisos mínimos y validación humana cuando corresponda.
