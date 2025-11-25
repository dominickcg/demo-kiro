# Guía del Proyecto Spec - Validador de Actas Electorales

**Duración:** ~90 minutos  
**Objetivo:** Aprender desarrollo estructurado con Kiro usando Specs, property-based testing, y características avanzadas

## Introducción

En esta parte de la demo construiremos un **Validador de Actas Electorales** usando el modo Spec de Kiro. A diferencia del modo Vibe, aquí seguiremos un proceso estructurado:

1. **Requirements** - Qué necesitamos construir
2. **Design** - Cómo lo vamos a construir
3. **Tasks** - Pasos específicos de implementación
4. **Implementation** - Construcción guiada por las tareas

## Fase 1: Explorar los Specs (10 minutos)

### Paso 1.1: Abrir Requirements

**Acción:**
```
Abre el archivo: .kiro/specs/demo-task-manager/requirements.md
```

**Qué observar:**
- Estructura con User Stories y Acceptance Criteria
- Formato EARS en cada criterio
- Glossary con términos definidos
- Requirements organizados por funcionalidad

**Reflexión:** Los requirements son el "contrato" de lo que vamos a construir.

### Paso 1.2: Revisar Design

**Acción:**
```
Abre el archivo: .kiro/specs/demo-task-manager/design.md
```

**Qué observar:**
- Arquitectura modular (Parser, Validator, Types, CLI)
- Interfaces y tipos de datos
- **Correctness Properties** - Propiedades que deben cumplirse
- Estrategia de testing con property-based tests

**Reflexión:** El diseño traduce requirements en una arquitectura técnica.

### Paso 1.3: Ver Task List

**Acción:**
```
Abre el archivo: .kiro/specs/demo-task-manager/tasks.md
```

**Qué observar:**
- Tareas numeradas y organizadas
- Cada tarea referencia requirements específicos
- Checkboxes para marcar progreso
- Tareas de testing integradas

**Reflexión:** Las tareas son el plan de implementación paso a paso.

---

## Fase 2: Setup del Proyecto (10 minutos)

### Paso 2.1: Inicializar Proyecto Node.js

**Prompt para Kiro:**
```
Crea un nuevo proyecto Node.js con TypeScript para el validador de actas. 
Incluye package.json con scripts para build, test, y dev.
Usa Vitest para testing y fast-check para property-based testing.
```

**Archivos esperados:**
- `package.json`
- `tsconfig.json`
- `.gitignore`

**Verificación:**
```bash
npm install
```

### Paso 2.2: Crear Estructura de Carpetas

**Prompt para Kiro:**
```
Crea la estructura de carpetas para el proyecto:
- src/ (código fuente)
- src/types/ (definiciones de tipos)
- src/parser/ (lógica de parseo)
- src/validator/ (lógica de validación)
- src/cli/ (interfaz de línea de comandos)
- tests/ (tests unitarios y de propiedades)
```

**Verificación:** Revisa que las carpetas existen en el explorador de archivos.

### Paso 2.3: Configurar Steering File

**¿Qué es un Steering File?**

Un steering file es un archivo de configuración que proporciona contexto y convenciones a Kiro. Funciona como "instrucciones permanentes" que Kiro consulta automáticamente cuando genera código.

**¿Por qué configurarlo ahora?**
- Ahorra tiempo: No repites las mismas instrucciones en cada prompt
- Mantiene consistencia: Todo el código sigue las mismas convenciones
- Ahorra tokens: Las convenciones no se incluyen en cada mensaje

**Ubicación:** `.kiro/steering/typescript-conventions.md`

**Prompt para Kiro:**
```
Crea .kiro/steering/typescript-conventions.md con el siguiente contenido:

# Convenciones de TypeScript para Validador de Actas

## Estilo de Código

### Naming Conventions
- Interfaces: PascalCase (ej: Acta, ValidationResult)
- Funciones y variables: camelCase (ej: parseActa, isValid)
- Constantes: UPPER_SNAKE_CASE (ej: MAX_FILE_SIZE)

### Type System
- Usar interface en lugar de type cuando sea posible
- Definir tipos de retorno explícitos en funciones públicas

### Async/Await
- Usar async/await en lugar de .then() para promesas
- Siempre manejar errores con try/catch en funciones async

## Estructura de Archivos
- Un componente/clase por archivo
- Archivos de tipos en carpeta types/
- Tests en archivos .test.ts junto al código

## Comentarios
- Comentarios inline en español para explicar lógica de negocio
- JSDoc en inglés para documentación de API pública

## Mensajes de Usuario
- Todos los mensajes mostrados al usuario deben estar en español
- Incluir valores específicos en los mensajes de error
```

**Verificación:** 
1. Abre `.kiro/steering/typescript-conventions.md`
2. Revisa que el contenido está completo

**Probar que funciona:**
```
Kiro, crea una función auxiliar que calcule el porcentaje de participación
```

Observa que Kiro usa camelCase, comentarios en español, y sigue las convenciones sin que las menciones.

**Beneficio:** A partir de ahora, todo el código generado será consistente automáticamente.

---

## Fase 3: Implementar Types (10 minutos)

### Paso 3.1: Crear Interfaces de Datos

**Prompt para Kiro:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea el archivo src/types/acta.ts con las interfaces:
- Acta (mesaId, votantesHabilitados, votosPorCandidato, totalVotos)
- VoteTally (candidatoId, nombreCandidato, votos)
- ValidationResult (isValid, errors)

Sigue las definiciones exactas del design document.
```

**Verificación:** Abre `src/types/acta.ts` y revisa que las interfaces coinciden con el diseño.

### Paso 3.2: Exportar Types

**Prompt para Kiro:**
```
Crea src/types/index.ts que exporte todas las interfaces de acta.ts
```

---

## Fase 4: Implementar Parser (15 minutos)

### Paso 4.1: Crear ActaParser

**Prompt para Kiro:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea src/parser/actaParser.ts con la clase ActaParser que incluya:
- readFile(filePath: string): Promise<string> - Lee archivo del sistema
- parseActa(jsonContent: string): Acta - Parsea JSON a objeto Acta
- validateFormat(jsonContent: string): boolean - Valida formato básico

Maneja errores según la sección Error Handling del design document.
Todos los mensajes de error deben estar en español.
```

**Verificación:** Revisa que los métodos existen y manejan errores correctamente.

### Paso 4.2: Probar Parser Manualmente

**Prompt para Kiro:**
```
Crea un script temporal test-parser.ts que:
1. Importe ActaParser
2. Lea el archivo examples/spec/valid-acta.json
3. Parsee el contenido
4. Imprima el resultado en consola
```

**Ejecutar:**
```bash
npx tsx test-parser.ts
```

**Resultado esperado:** Debe mostrar el objeto Acta parseado correctamente.

---

## Fase 5: Implementar Validator (20 minutos)

### Paso 5.1: Crear ActaValidator

**Prompt para Kiro:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea src/validator/actaValidator.ts con la clase ActaValidator que incluya:
- validate(acta: Acta): ValidationResult - Método principal
- validateSumConsistency(acta: Acta): string | null - Verifica suma
- validateNoNegativeVotes(acta: Acta): string | null - Verifica no negativos
- validateTotalVsEnabled(acta: Acta): string | null - Verifica total vs habilitados

El método validate debe ejecutar todas las validaciones y acumular errores.
Usa los mensajes de error exactos del design document en español.
```

**Verificación:** Revisa que cada método de validación retorna el mensaje correcto.

### Paso 5.2: Probar Validator con Ejemplos

**Prompt para Kiro:**
```
Crea un script test-validator.ts que:
1. Parsee los 3 archivos de ejemplo (valid, invalid, anomaly)
2. Valide cada uno con ActaValidator
3. Imprima los resultados

Usa los archivos:
- examples/spec/valid-acta.json (debe pasar)
- examples/spec/invalid-acta.json (debe fallar)
- examples/spec/anomaly-acta.json (debe fallar)
```

**Ejecutar:**
```bash
npx tsx test-validator.ts
```

**Resultado esperado:**
- valid-acta: `isValid: true, errors: []`
- invalid-acta: `isValid: false, errors: [...]` (suma incorrecta, voto negativo)
- anomaly-acta: `isValid: false, errors: [...]` (total excede habilitados)

---

## Fase 6: Implementar CLI (10 minutos)

### Paso 6.1: Crear Interfaz CLI

**Prompt para Kiro:**
```
Crea src/cli/index.ts que:
1. Acepte un argumento de línea de comandos (ruta al archivo de acta)
2. Use ActaParser para leer y parsear el archivo
3. Use ActaValidator para validar el acta
4. Imprima el resultado formateado en español:
   - Si es válida: "✓ Acta válida: [mesaId]"
   - Si es inválida: "✗ Acta inválida: [mesaId]" seguido de lista de errores
5. Maneje errores de archivo no encontrado o JSON inválido

Agrega un script "validate" en package.json que ejecute este CLI.
```

**Verificación:** Revisa que el script está en package.json.

### Paso 6.2: Probar CLI

**Ejecutar:**
```bash
npm run validate examples/spec/valid-acta.json
npm run validate examples/spec/invalid-acta.json
npm run validate examples/spec/anomaly-acta.json
```

**Resultado esperado:** Mensajes formateados en español mostrando validación correcta.

---

## CHECKPOINT 1: Funcionalidad Básica Completa

**Verificar:**
- Parser lee y parsea archivos JSON
- Validator detecta inconsistencias
- CLI funciona con los 3 ejemplos
- Mensajes de error en español

**Si algo falla:** Pide a Kiro que revise y corrija el componente específico.

---

## Fase 7: Property-Based Testing (25 minutos)

### ¿Qué es Property-Based Testing?

En lugar de escribir tests con ejemplos específicos, definimos **propiedades** que deben cumplirse para **cualquier** entrada válida. El framework (fast-check) genera automáticamente cientos de casos de prueba aleatorios.

**Ejemplo:**
- Test tradicional: "El acta con votos [120, 95, 10] y total 225 es válida"
- Property test: "Para cualquier acta donde suma = total y sin negativos, debe ser válida"

### Paso 7.1: Crear Generadores de Datos

**Prompt para Kiro:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea tests/generators.ts con generadores de fast-check para:

1. validActaArbitrary - Genera actas válidas donde:
   - mesaId es un string aleatorio
   - votantesHabilitados entre 100-1000
   - 2-10 candidatos con votos entre 0-200
   - totalVotos = suma exacta de votos individuales

2. invalidSumActaArbitrary - Genera actas donde suma ≠ totalVotos

3. negativeVotesActaArbitrary - Genera actas con al menos un voto negativo

4. exceedsEnabledActaArbitrary - Genera actas donde totalVotos > votantesHabilitados

Usa fc.record, fc.array, fc.integer, fc.string de fast-check.
```

**Verificación:** Revisa que los generadores usan las funciones correctas de fast-check.

### Paso 7.2: Implementar Property Tests

**Prompt para Kiro:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea tests/validator.property.test.ts con property tests para:

**Property 6: Validación de consistencia de suma**
// **Feature: demo-task-manager, Property 6: Validación de consistencia de suma**
- Usa invalidSumActaArbitrary
- Verifica que isValid=false y errors contiene "suma"
- Configura 100 iteraciones

**Property 7: Detección de votos negativos**
// **Feature: demo-task-manager, Property 7: Detección de votos negativos**
- Usa negativeVotesActaArbitrary
- Verifica que isValid=false y errors contiene "negativo"
- Configura 100 iteraciones

**Property 8: Validación de total vs habilitados**
// **Feature: demo-task-manager, Property 8: Validación de total vs habilitados**
- Usa exceedsEnabledActaArbitrary
- Verifica que isValid=false y errors contiene "excede"
- Configura 100 iteraciones

**Property 10: Actas válidas pasan validación**
// **Feature: demo-task-manager, Property 10: Actas válidas pasan validación**
- Usa validActaArbitrary
- Verifica que isValid=true y errors.length === 0
- Configura 100 iteraciones

Usa fc.assert y fc.property de fast-check.
Cada test debe tener el comentario con el formato especificado.
```

**Verificación:** Revisa que cada test tiene el comentario de anotación correcto.

### Paso 7.3: Ejecutar Property Tests

**Ejecutar:**
```bash
npm test
```

**Resultado esperado:**
- Todos los property tests pasan
- Cada test ejecuta 100 iteraciones
- Si alguno falla, fast-check muestra el contraejemplo que causó el fallo

**Si un test falla:**
```
Kiro, el property test [nombre] está fallando con este contraejemplo: [pegar output]
¿Puedes revisar el generador o la lógica de validación?
```

### Paso 7.4: Implementar Property Test de Round-Trip

**Prompt para Kiro:**
```
Agrega a tests/validator.property.test.ts:

**Property 11: Round-trip de serialización**
// **Feature: demo-task-manager, Property 11: Round-trip de serialización**
- Usa validActaArbitrary
- Serializa a JSON con JSON.stringify
- Parsea de vuelta con JSON.parse
- Verifica que el objeto resultante es equivalente al original
- Configura 100 iteraciones
```

**Ejecutar:**
```bash
npm test
```

---

## CHECKPOINT 2: Property Tests Completos

**Verificar:**
- 4 property tests implementados y pasando
- Cada test ejecuta 100 iteraciones
- Comentarios de anotación presentes
- Generadores producen datos válidos

---

## Fase 8: Configurar Agent Hook (5 minutos)

**¿Qué es un Agent Hook?**

Los agent hooks son automatizaciones que ejecutan acciones en respuesta a eventos. Son como "triggers" que responden a cambios en tu proyecto.

**¿Por qué configurarlo ahora?**
- Ya tienes tests implementados (algo que ejecutar)
- Detectarás errores inmediatamente al guardar
- No necesitas ejecutar tests manualmente cada vez

**Tipos de eventos disponibles:**
- **onFileSave:** Se dispara cuando guardas un archivo
- **onMessage:** Se dispara cuando envías un mensaje a Kiro
- **onSessionStart:** Se dispara cuando inicias una sesión
- **Manual:** Se dispara cuando haces clic en un botón

**Configuración paso a paso:**

1. **Abrir panel de Agent Hooks:**
   - Busca "Agent Hooks" en la barra lateral de Kiro
   - O usa Command Palette: `Ctrl+Shift+P` → "Open Kiro Hook UI"

2. **Crear nuevo hook:**
   - Haz clic en "Create New Hook" o botón "+"

3. **Configurar el hook:**
   - **Name:** `Ejecutar tests al guardar`
   - **Trigger:** `onFileSave`
   - **File Pattern:** `**/*.ts` (todos los archivos TypeScript)
   - **Action Type:** `Command`
   - **Command:** `npm test`
   - **Enabled:** ✓ (marcado)

4. **Guardar:** Haz clic en "Save" o "Create"

**Probar que funciona:**

1. Abre cualquier archivo `.ts` (por ejemplo `src/validator/actaValidator.ts`)
2. Haz un cambio pequeño (agrega un comentario)
3. Guarda el archivo (`Ctrl+S`)
4. Observa la terminal: los tests se ejecutan automáticamente

**Resultado esperado:**
```
> npm test

Running tests...
✓ All tests passed
```

**Patrones de File Pattern útiles:**

| Pattern | Descripción |
|---------|-------------|
| `**/*.ts` | Todos los archivos TypeScript |
| `src/**/*.ts` | Solo TypeScript en src/ |
| `**/*.test.ts` | Solo archivos de test |
| `**/*.{ts,js}` | TypeScript o JavaScript |

**Beneficio:** Ahora detectarás errores inmediatamente sin ejecutar tests manualmente. Es como tener un asistente que verifica tu código constantemente.

---

## Fase 9: Unit Tests (15 minutos)

### Paso 8.1: Tests del Parser

**Prompt para Kiro:**
```
Crea tests/parser.test.ts con unit tests para:
1. Parseo exitoso de acta válida
2. Error cuando archivo no existe
3. Error cuando JSON es inválido
4. Error cuando faltan campos requeridos

Usa los archivos de examples/spec/ para los tests.
```

### Paso 8.2: Tests del Validator

**Prompt para Kiro:**
```
Crea tests/validator.test.ts con unit tests para:
1. Acta válida pasa validación
2. Acta con suma incorrecta falla
3. Acta con voto negativo falla
4. Acta con total > habilitados falla
5. Acta con múltiples errores reporta todos

Usa ejemplos específicos con valores conocidos.
```

### Paso 8.3: Ejecutar Todos los Tests

**Ejecutar:**
```bash
npm test
```

**Resultado esperado:** Todos los tests (unit + property) pasan.

---

## Fase 10: Configurar MCP Server (Opcional - 10 minutos)

**¿Qué es MCP?**

MCP (Model Context Protocol) es un protocolo que permite a Kiro conectarse con herramientas y servicios externos. Piensa en MCP como "plugins" que le dan a Kiro nuevas capacidades.

**¿Para qué sirve?**
- Acceso a sistemas externos (bases de datos, APIs)
- Herramientas especializadas (análisis de código, búsqueda avanzada)
- Integración con servicios (GitHub, Slack, etc.)

**Nota:** Esta sección es opcional. MCP es útil para integraciones avanzadas pero no es necesario para el proyecto básico.

### Paso 10.1: Instalar uvx (si no lo tienes)

MCP servers se ejecutan con `uvx`, que requiere `uv` (gestor de paquetes Python).

**Verificar si está instalado:**
```bash
uv --version
```

**Si no está instalado:**

Windows:
```bash
pip install uv
```

macOS/Linux:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Paso 10.2: Configurar MCP Server Filesystem

**Crear archivo:** `.kiro/settings/mcp.json`

**Prompt para Kiro:**
```
Crea .kiro/settings/mcp.json con esta configuración:

{
  "mcpServers": {
    "filesystem": {
      "command": "uvx",
      "args": ["mcp-server-filesystem"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "disabled": false,
      "autoApprove": ["read_file", "list_directory"]
    }
  }
}
```

**¿Qué hace cada parte?**
- `command`: Ejecutable que inicia el servidor
- `args`: Argumentos para el comando
- `env`: Variables de entorno
- `disabled`: Si está activo o no
- `autoApprove`: Herramientas que no piden confirmación

### Paso 10.3: Verificar Conexión

**Método 1: Panel de MCP Servers**
1. Abre el panel de MCP Servers en Kiro
2. Busca "filesystem" en la lista
3. Verifica el estado: ✓ Conectado

**Método 2: Command Palette**
1. `Ctrl+Shift+P` → "View MCP Servers"
2. Revisa el estado de cada servidor

**Si no se conecta:**
- Verifica que `uvx` está instalado
- Revisa la sintaxis del JSON
- Reconecta desde el panel de MCP

### Paso 10.4: Usar Herramientas MCP

**Ejemplo 1: Listar archivos**
```
Usando herramientas MCP, lista los archivos en examples/spec/
```

**Resultado esperado:**
```
- valid-acta.json
- invalid-acta.json
- anomaly-acta.json
```

**Ejemplo 2: Leer archivo**
```
Usando MCP, lee el contenido de examples/spec/valid-acta.json
```

**Herramientas disponibles del servidor filesystem:**
- `read_file` - Leer contenido de archivos
- `write_file` - Escribir en archivos
- `list_directory` - Listar contenido de carpetas
- `create_directory` - Crear carpetas
- `move_file` - Mover/renombrar archivos

### Paso 10.5: AutoApprove (Importante)

**¿Qué es autoApprove?**

Por defecto, Kiro pide confirmación antes de usar herramientas MCP. Con `autoApprove`, especificas herramientas que se ejecuten sin confirmación.

**Usar autoApprove para:**
- Operaciones de solo lectura (`read_file`, `list_directory`)
- Herramientas que usas frecuentemente
- Operaciones seguras sin efectos secundarios

**NO usar autoApprove para:**
- Operaciones de escritura (`write_file`, `delete_file`)
- Operaciones destructivas
- Herramientas que modifican datos externos

**Beneficio de MCP:** Kiro puede explorar el sistema de archivos de forma más flexible y acceder a herramientas especializadas según tus necesidades.

---

## Fase 11: Integración y Documentación (10 minutos)

### Paso 10.1: Crear README del Proyecto

**Prompt para Kiro:**
```
Crea un README.md para el proyecto que incluya:
- Descripción del validador de actas
- Requisitos (Node.js, npm)
- Instalación (npm install)
- Uso (npm run validate <archivo>)
- Ejecución de tests (npm test)
- Estructura del proyecto
- Ejemplos de uso con los archivos de examples/spec/
```

### Paso 10.2: Agregar Scripts Útiles

**Prompt para Kiro:**
```
Agrega estos scripts a package.json:
- "lint": Ejecutar linter (eslint)
- "format": Formatear código (prettier)
- "test:watch": Ejecutar tests en modo watch
- "test:coverage": Generar reporte de cobertura
```

---

## CHECKPOINT FINAL: Proyecto Completo

**Verificar:**
- Código funcional con parser, validator, y CLI
- Property tests implementados y pasando
- Unit tests implementados y pasando
- Steering file configurado (Fase 2)
- Agent hook funcionando (Fase 8)
- MCP configurado (opcional)
- README documentado
- Todos los tests pasan

---

## Reflexión: Modo Spec vs Modo Vibe

### Ventajas del Modo Spec

✅ **Documentación clara:** Requirements y design sirven como referencia  
✅ **Correctitud garantizada:** Property tests validan comportamiento general  
✅ **Mantenibilidad:** Arquitectura modular y bien estructurada  
✅ **Trazabilidad:** Cada tarea referencia requirements específicos  
✅ **Escalabilidad:** Fácil agregar nuevas validaciones o features  

### Cuándo Usar Modo Spec

- Proyectos de producción
- Código que requiere alta confiabilidad
- Proyectos con múltiples desarrolladores
- Sistemas con requisitos complejos
- Cuando necesitas documentación formal

### Cuándo Usar Modo Vibe

- Prototipos rápidos
- Experimentos y pruebas de concepto
- Scripts de una sola vez
- Aprendizaje y exploración
- Proyectos personales pequeños

---

## Recursos Adicionales

- **EARS Guide:** Formato de requirements estructurados
- **FAQ:** Preguntas frecuentes sobre Kiro
- **Best Practices:** Mejores prácticas de uso de Kiro
- **Advanced Features:** Características avanzadas de Kiro

---

## Siguiente Paso

Ahora que completaste el proyecto Spec, puedes:
1. Explorar características avanzadas (sesiones múltiples, #Codebase avanzado)
2. Configurar GitHub y CI/CD para el proyecto
3. Practicar con tus propios proyectos

¡Felicitaciones por completar el proyecto Spec! 🎉
