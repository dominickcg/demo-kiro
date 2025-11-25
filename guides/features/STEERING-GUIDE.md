# Guía de Steering Files

**Duración:** 5-10 minutos  
**Objetivo:** Aprender a configurar steering files para que Kiro siga convenciones específicas de tu proyecto

## ¿Qué son los Steering Files?

Los **steering files** son archivos de configuración que proporcionan contexto y convenciones a Kiro. Funcionan como "instrucciones permanentes" que Kiro consulta automáticamente cuando genera código.

### ¿Para qué sirven?

- **Mantener consistencia:** Todos en el equipo siguen las mismas convenciones
- **Ahorrar tokens:** No necesitas repetir las mismas instrucciones en cada prompt
- **Documentar decisiones:** Las convenciones quedan registradas en el proyecto
- **Acelerar desarrollo:** Kiro genera código que ya cumple tus estándares

### Ejemplos de uso

- Convenciones de estilo de código (naming, formatting)
- Patrones de diseño preferidos (repository pattern, factory pattern)
- Estructura de archivos y carpetas
- Librerías y frameworks a usar
- Mensajes de error y logging
- Referencias a documentación externa (APIs, specs)

---

## Ubicación de Steering Files

Los steering files se guardan en:
```
.kiro/steering/
```

Puedes crear múltiples archivos para organizar diferentes tipos de convenciones:
- `typescript-conventions.md` - Convenciones de TypeScript
- `api-guidelines.md` - Guías para APIs
- `testing-standards.md` - Estándares de testing
- `ui-patterns.md` - Patrones de UI

---

## Cuándo Configurar Steering Files

⏰ **Momento ideal:** Al inicio del proyecto, antes de escribir código

**Flujo recomendado:**
1. Crear proyecto
2. Configurar steering files
3. Comenzar a desarrollar con Kiro

**Nota:** También puedes agregar steering files en cualquier momento del proyecto.

---

## Ejemplo Completo: TypeScript Conventions

### Crear el Steering File

**Ubicación:** `.kiro/steering/typescript-conventions.md`

**Contenido:**

```markdown
# Convenciones de TypeScript para Validador de Actas

## Estilo de Código

### Naming Conventions
- **Interfaces:** PascalCase (ej: `Acta`, `ValidationResult`)
- **Clases:** PascalCase (ej: `ActaParser`, `ActaValidator`)
- **Funciones y variables:** camelCase (ej: `parseActa`, `isValid`)
- **Constantes:** UPPER_SNAKE_CASE (ej: `MAX_FILE_SIZE`)
- **Archivos:** kebab-case (ej: `acta-parser.ts`)

### Type System
- Usar `interface` en lugar de `type` cuando sea posible
- Preferir tipos explícitos sobre `any`
- Usar `unknown` en lugar de `any` cuando el tipo es desconocido
- Definir tipos de retorno explícitos en funciones públicas

### Async/Await
- Usar `async/await` en lugar de `.then()` para promesas
- Siempre manejar errores con try/catch en funciones async
- Nombrar funciones async con verbos claros (ej: `readFile`, `validateActa`)

## Estructura de Archivos

### Organización
- Un componente/clase por archivo
- Archivos de tipos en carpeta `types/`
- Tests en archivos `.test.ts` junto al código fuente
- Archivos de utilidades en carpeta `utils/`

### Imports
- Imports de librerías externas primero
- Imports de módulos internos después
- Ordenar alfabéticamente dentro de cada grupo
- Usar imports absolutos desde `src/`

Ejemplo:
```typescript
// Librerías externas
import { readFile } from 'fs/promises';
import { join } from 'path';

// Módulos internos
import { Acta, ValidationResult } from '@/types';
import { ActaParser } from '@/parser';
```

## Comentarios y Documentación

### Comentarios en Español
- Comentarios inline en español para explicar lógica de negocio
- Comentarios en español para algoritmos complejos
- Comentarios en español para decisiones de diseño no obvias

### JSDoc en Inglés
- JSDoc en inglés para documentación de API pública
- Incluir tipos, parámetros, y valores de retorno
- Agregar ejemplos de uso cuando sea útil

Ejemplo:
```typescript
/**
 * Validates an electoral acta for mathematical consistency
 * @param acta - The acta to validate
 * @returns Validation result with errors if any
 */
validate(acta: Acta): ValidationResult {
  // Validar que la suma de votos coincide con el total declarado
  const sumError = this.validateSumConsistency(acta);
  // ...
}
```

## Manejo de Errores

### Mensajes de Error
- Todos los mensajes mostrados al usuario deben estar en español
- Incluir valores específicos en los mensajes (ej: valores esperados vs recibidos)
- Usar formato descriptivo: `Error: [descripción] - [detalles]`

Ejemplo:
```typescript
throw new Error(`Error: La suma de votos individuales (${suma}) no coincide con el total declarado (${totalVotos})`);
```

### Error Handling
- Usar clases de error personalizadas cuando sea apropiado
- Capturar errores específicos antes que genéricos
- Siempre propagar errores con contexto útil

## Testing

### Naming
- Archivos de test: `[nombre].test.ts`
- Property tests: `[nombre].property.test.ts`
- Nombres de tests descriptivos en español

### Estructura
- Usar `describe` para agrupar tests relacionados
- Usar `it` o `test` para casos individuales
- Configurar property tests con mínimo 100 iteraciones

Ejemplo:
```typescript
describe('ActaValidator', () => {
  it('debe validar correctamente un acta válida', () => {
    // ...
  });
  
  it('debe detectar votos negativos', () => {
    // ...
  });
});
```

## Mensajes de Usuario

### Idioma
- Todos los mensajes mostrados al usuario: **español**
- Código, variables, funciones: **inglés**
- Comentarios de lógica de negocio: **español**

### Formato
- Usar símbolos para indicar estado: ✓ (éxito), ✗ (error), ⚠️ (advertencia)
- Mensajes claros y concisos
- Incluir información contextual relevante

Ejemplo:
```typescript
console.log(`✓ Acta válida: ${acta.mesaId}`);
console.log(`✗ Acta inválida: ${acta.mesaId}`);
console.log(`  - Error: ${error}`);
```

## Dependencias

### Librerías Preferidas
- **Testing:** Vitest (unit tests) + fast-check (property-based testing)
- **Linting:** ESLint con configuración TypeScript
- **Formatting:** Prettier
- **File I/O:** fs/promises (async)

### Evitar
- Librerías obsoletas o sin mantenimiento
- Dependencias pesadas para tareas simples
- Múltiples librerías que hacen lo mismo
```

---

## Cómo Crear tu Steering File

### Paso 1: Crear el Archivo

**Prompt para Kiro:**
```
Crea el archivo .kiro/steering/typescript-conventions.md con convenciones para este proyecto
```

### Paso 2: Definir Convenciones

Incluye secciones para:
- ✅ Estilo de código (naming, formatting)
- ✅ Estructura de archivos
- ✅ Manejo de errores
- ✅ Testing
- ✅ Documentación
- ✅ Dependencias preferidas

### Paso 3: Ser Específico

❌ **Vago:** "Usar buenos nombres de variables"  
✅ **Específico:** "Variables en camelCase, constantes en UPPER_SNAKE_CASE"

❌ **Vago:** "Escribir tests"  
✅ **Específico:** "Property tests con mínimo 100 iteraciones usando fast-check"

---

## Verificar que Kiro Usa el Steering File

### Prueba 1: Generar Código Nuevo

**Prompt:**
```
Crea una nueva función auxiliar que calcule el porcentaje de participación electoral
```

**Verificar:**
- ¿Usa camelCase para el nombre?
- ¿Tiene comentarios en español?
- ¿Sigue la estructura definida?

### Prueba 2: Pedir Refactoring

**Prompt:**
```
Refactoriza la función validateActa para mejorar legibilidad
```

**Verificar:**
- ¿Mantiene las convenciones?
- ¿Usa los patrones definidos?

### Prueba 3: Generar Tests

**Prompt:**
```
Crea tests para la nueva función de porcentaje de participación
```

**Verificar:**
- ¿Usa Vitest?
- ¿Nombres de tests en español?
- ¿Estructura correcta?

---

## Steering Files Avanzados

### Incluir Referencias Externas

Puedes referenciar archivos externos usando la sintaxis:
```markdown
#[[file:openapi-spec.yaml]]
```

Esto es útil para:
- Especificaciones de API (OpenAPI, GraphQL)
- Esquemas de base de datos
- Documentación de protocolos
- Gramáticas de parsers

**Ejemplo:**
```markdown
# API Guidelines

Seguir la especificación OpenAPI del proyecto:
#[[file:docs/api-spec.yaml]]

Todas las rutas deben:
- Usar versionado (ej: /api/v1/...)
- Retornar JSON
- Incluir códigos de estado HTTP apropiados
```

### Steering Files Condicionales

Puedes crear steering files que solo se incluyen cuando se trabaja con archivos específicos:

**Front matter:**
```markdown
---
inclusion: fileMatch
fileMatchPattern: '**/*.test.ts'
---

# Testing Guidelines

Este steering file solo se activa cuando trabajas con archivos de test...
```

### Steering Files Manuales

Para steering files que solo quieres incluir explícitamente:

**Front matter:**
```markdown
---
inclusion: manual
---

# Advanced Patterns

Este steering file solo se incluye cuando lo referencias con #...
```

---

## Mejores Prácticas

### ✅ Hacer

- Crear steering files al inicio del proyecto
- Ser específico y dar ejemplos
- Actualizar cuando cambien las convenciones
- Incluir el "por qué" de decisiones importantes
- Usar múltiples archivos para organizar por tema

### ❌ Evitar

- Steering files demasiado largos (dividir en múltiples)
- Convenciones contradictorias entre archivos
- Información obsoleta o incorrecta
- Ser demasiado restrictivo (dejar espacio para flexibilidad)

---

## Ejemplo de Uso en la Demo

Durante el proyecto Spec, el steering file asegura que:

1. **Paso de Types:** Interfaces en PascalCase, exports organizados
2. **Paso de Parser:** Manejo de errores en español, async/await
3. **Paso de Validator:** Mensajes descriptivos, métodos privados claros
4. **Paso de Tests:** Vitest + fast-check, nombres en español

**Resultado:** Código consistente sin repetir instrucciones en cada prompt.

---

## Recursos Adicionales

- **Documentación oficial:** Consulta la documentación de Kiro sobre steering files
- **Ejemplos:** Revisa proyectos open source que usan Kiro
- **Comunidad:** Comparte tus steering files con el equipo

---

## Siguiente Paso

Ahora que entiendes steering files, puedes:
1. Crear steering files para tus proyectos
2. Compartir steering files con tu equipo
3. Explorar Agent Hooks para automatización adicional

**Archivo relacionado:** [HOOKS-GUIDE.md](HOOKS-GUIDE.md) - Aprende sobre automatización con hooks
