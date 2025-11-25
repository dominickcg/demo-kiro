# Guía Maestra de la Demo Kiro

**Duración total:** 2 horas (120 minutos)  
**Audiencia:** Entidades de procesos electorales  
**Nivel:** Básico a Intermedio

---

## 📋 Resumen Ejecutivo

Esta demo muestra las capacidades de Kiro a través de dos proyectos prácticos relacionados con procesos electorales:

1. **Modo Vibe (15 min):** Generador de reportes de participación - desarrollo rápido
2. **Modo Spec (105 min):** Validador de actas electorales - desarrollo estructurado

**Objetivo:** Que los participantes aprendan a usar Kiro efectivamente y puedan aplicarlo en sus proyectos.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar la demo, los participantes podrán:

- ✅ Distinguir entre modo Vibe y modo Spec
- ✅ Crear y usar specs (requirements, design, tasks)
- ✅ Implementar property-based testing
- ✅ Configurar steering files, hooks y MCP servers
- ✅ Aplicar mejores prácticas de uso de Kiro
- ✅ Optimizar consumo de tokens

---

## 📦 Preparación (30 minutos antes)

### Checklist del Instructor

**Entorno:**
- [ ] Kiro instalado y funcionando
- [ ] Node.js v18+ instalado
- [ ] Terminal lista y configurada
- [ ] Repositorio clonado localmente
- [ ] Conexión a internet estable

**Materiales:**
- [ ] README.md abierto en navegador
- [ ] FAQ.md accesible para consulta rápida
- [ ] Todas las guías revisadas
- [ ] Ejemplos de archivos verificados (CSV y JSON)

**Proyector/Pantalla:**
- [ ] Resolución adecuada para código
- [ ] Fuente de código legible (tamaño 14-16pt)
- [ ] Terminal visible claramente
- [ ] Panel de Kiro visible

**Backup:**
- [ ] Código de ejemplo pre-generado (por si falla algo)
- [ ] Capturas de pantalla de resultados esperados
- [ ] Plan B si internet falla

---

## ⏱️ Timeline Minuto a Minuto

### Minutos 0-5: Introducción y Setup

**Objetivos:**
- Presentar Kiro y la agenda
- Verificar que todos tienen el entorno listo

**Script sugerido:**
```
"Bienvenidos a esta demo de Kiro. En las próximas 2 horas vamos a aprender 
a usar Kiro para desarrollo de software, usando ejemplos del contexto electoral.

Vamos a construir dos proyectos:
1. Un generador de reportes de participación (modo rápido)
2. Un validador de actas electorales (modo estructurado)

¿Todos tienen Kiro instalado? ¿Node.js? Perfecto, comencemos."
```

**Acciones:**
- Mostrar la estructura del repositorio
- Abrir README.md y explicar la organización
- Verificar que participantes pueden seguir

**Checkpoint:** Todos tienen el repositorio abierto en Kiro

---

### Minutos 5-20: PARTE 1 - Modo Vibe

**Guía:** [VIBE-GUIDE.md](projects/VIBE-GUIDE.md)

#### Minutos 5-8: Introducción al Modo Vibe

**Script sugerido:**
```
"Modo Vibe es desarrollo rápido sin documentación formal. 
Perfecto para prototipos y experimentos.

Vamos a crear un generador de reportes que lea datos de participación 
desde un CSV y genere estadísticas."
```

**Acciones:**
- Mostrar archivo `examples/vibe/turnout-data.csv`
- Explicar qué vamos a construir
- Abrir nueva sesión en Kiro

#### Minutos 8-15: Desarrollo Iterativo

**Prompt 1:**
```
Crea un script Node.js que lea el archivo examples/vibe/turnout-data.csv 
y genere un reporte de participación electoral con:
- Total de votantes habilitados
- Total de votos emitidos
- Porcentaje de participación
- Datos por mesa
```

**Acciones:**
- Ejecutar el código generado
- Mostrar el reporte

**Prompt 2:**
```
Agrega detección de anomalías: marca las mesas donde 
los votos emitidos exceden los votantes habilitados
```

**Acciones:**
- Ejecutar de nuevo
- Mostrar la detección de anomalías

**Prompt 3:**
```
Formatea el reporte como una tabla legible con columnas alineadas
```

**Acciones:**
- Ejecutar y mostrar resultado final

#### Minutos 15-20: Reflexión sobre Modo Vibe

**Script sugerido:**
```
"Vieron qué rápido fue? En 10 minutos tenemos un reporte funcional.

Ventajas:
- Muy rápido
- Ideal para prototipos
- Iteración inmediata

Desventajas:
- Sin tests
- Sin documentación
- No garantiza correctitud
- Difícil de mantener

Para proyectos de producción, necesitamos algo más robusto. 
Ahí entra el Modo Spec."
```

**Checkpoint:** Todos entienden las ventajas y limitaciones del modo Vibe

---

### Minutos 20-25: Ejercicio EARS

**Guía:** [EARS-GUIDE.md](projects/EARS-GUIDE.md)

**Script sugerido:**
```
"Antes de entrar al modo Spec, necesitamos entender EARS.
EARS es un formato para escribir requirements sin ambigüedades.
Kiro lo usa como estándar."
```

**Acciones:**
- Mostrar los 6 patrones EARS
- Hacer ejercicio interactivo con Kiro

**Ejercicio:**
```
Prompt: "Convierte este requirement a formato EARS con criterios medibles:
'El sistema debe validar actas rápido'"

Respuesta esperada: "WHEN se valida un acta THEN el sistema SHALL 
completar la validación en menos de 2 segundos"
```

**Checkpoint:** Participantes entienden formato EARS

---

### Minutos 25-35: PARTE 2 - Explorar Specs

**Guía:** [SPEC-GUIDE.md](projects/SPEC-GUIDE.md) - Fase 1

**Script sugerido:**
```
"Ahora vamos a trabajar con modo Spec. Ya tenemos los specs creados,
vamos a explorarlos para entender la estructura."
```

#### Minutos 25-30: Requirements

**Acciones:**
- Abrir `.kiro/specs/demo-task-manager/requirements.md`
- Mostrar estructura: User Stories + Acceptance Criteria
- Señalar uso de formato EARS
- Mostrar Glossary

**Puntos clave:**
- Requirements definen QUÉ construir
- Formato EARS elimina ambigüedades
- Glossary define términos técnicos

#### Minutos 30-33: Design

**Acciones:**
- Abrir `.kiro/specs/demo-task-manager/design.md`
- Mostrar arquitectura modular
- Explicar Correctness Properties
- Mostrar estrategia de testing

**Puntos clave:**
- Design define CÓMO construir
- Arquitectura modular (Parser, Validator, Types, CLI)
- Correctness Properties para testing

#### Minutos 33-35: Tasks

**Acciones:**
- Abrir `.kiro/specs/demo-task-manager/tasks.md`
- Mostrar estructura de tareas
- Explicar cómo ejecutar tareas con Kiro

**Puntos clave:**
- Tasks son el plan de implementación
- Cada tarea referencia requirements
- Se ejecutan una por una

**Checkpoint:** Participantes entienden la estructura de specs

---

### Minutos 35-50: Setup e Implementación de Types

**Guía:** [SPEC-GUIDE.md](projects/SPEC-GUIDE.md) - Fases 2 y 3

#### Minutos 35-40: Setup del Proyecto

**Prompt:**
```
Crea un nuevo proyecto Node.js con TypeScript para el validador de actas. 
Incluye package.json con scripts para build, test, y dev.
Usa Vitest para testing y fast-check para property-based testing.
```

**Acciones:**
- Ejecutar `npm install`
- Verificar que se instaló correctamente

#### Minutos 40-45: Implementar Types

**Prompt:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea el archivo src/types/acta.ts con las interfaces:
- Acta (mesaId, votantesHabilitados, votosPorCandidato, totalVotos)
- VoteTally (candidatoId, nombreCandidato, votos)
- ValidationResult (isValid, errors)
```

**Acciones:**
- Revisar código generado
- Verificar que coincide con el diseño

#### Minutos 45-50: Configurar Steering File

**Guía:** [STEERING-GUIDE.md](features/STEERING-GUIDE.md)

**Script sugerido:**
```
"Antes de continuar, vamos a configurar un steering file.
Esto le dice a Kiro qué convenciones seguir automáticamente."
```

**Prompt:**
```
Crea .kiro/steering/typescript-conventions.md con convenciones:
- Interfaces en PascalCase
- Funciones en camelCase
- Mensajes de usuario en español
- Usar async/await
- Comentarios de lógica en español
```

**Checkpoint:** Types implementados y steering file configurado

---

### Minutos 50-70: Implementar Parser y Validator

**Guía:** [SPEC-GUIDE.md](projects/SPEC-GUIDE.md) - Fases 4 y 5

#### Minutos 50-60: Implementar Parser

**Prompt:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea src/parser/actaParser.ts con la clase ActaParser que incluya:
- readFile(filePath: string): Promise<string>
- parseActa(jsonContent: string): Acta
- validateFormat(jsonContent: string): boolean

Maneja errores según el design document. Mensajes en español.
```

**Acciones:**
- Revisar código generado
- Probar con `examples/spec/valid-acta.json`

#### Minutos 60-70: Implementar Validator

**Prompt:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea src/validator/actaValidator.ts con la clase ActaValidator que incluya:
- validate(acta: Acta): ValidationResult
- validateSumConsistency(acta: Acta): string | null
- validateNoNegativeVotes(acta: Acta): string | null
- validateTotalVsEnabled(acta: Acta): string | null

Usa los mensajes de error del design document en español.
```

**Acciones:**
- Revisar código generado
- Probar con los 3 archivos de ejemplo

**Checkpoint:** Parser y Validator funcionando

---

### Minutos 70-75: Implementar CLI

**Guía:** [SPEC-GUIDE.md](projects/SPEC-GUIDE.md) - Fase 6

**Prompt:**
```
Crea src/cli/index.ts que:
1. Acepte ruta al archivo como argumento
2. Use ActaParser para leer y parsear
3. Use ActaValidator para validar
4. Imprima resultado formateado en español

Agrega script "validate" en package.json
```

**Acciones:**
- Probar CLI con los 3 ejemplos:
  ```bash
  npm run validate examples/spec/valid-acta.json
  npm run validate examples/spec/invalid-acta.json
  npm run validate examples/spec/anomaly-acta.json
  ```

**Checkpoint:** CLI funcional con los 3 ejemplos

---

### Minutos 75-95: Property-Based Testing

**Guía:** [SPEC-GUIDE.md](projects/SPEC-GUIDE.md) - Fase 7

#### Minutos 75-80: Explicar Property-Based Testing

**Script sugerido:**
```
"Property-based testing es diferente a tests tradicionales.

Test tradicional:
'El acta con votos [120, 95, 10] y total 225 es válida'

Property test:
'Para CUALQUIER acta donde suma = total y sin negativos, debe ser válida'

El framework genera cientos de casos aleatorios automáticamente."
```

#### Minutos 80-90: Implementar Generadores

**Prompt:**
```
Usando #File .kiro/specs/demo-task-manager/design.md

Crea tests/generators.ts con generadores de fast-check para:
1. validActaArbitrary - Actas válidas
2. invalidSumActaArbitrary - Suma incorrecta
3. negativeVotesActaArbitrary - Votos negativos
4. exceedsEnabledActaArbitrary - Total > habilitados
```

#### Minutos 90-95: Implementar Property Tests

**Prompt:**
```
Crea tests/validator.property.test.ts con property tests para:

Property 6: Validación de consistencia de suma
Property 7: Detección de votos negativos
Property 8: Validación de total vs habilitados
Property 10: Actas válidas pasan validación

Cada test con 100 iteraciones y comentario de anotación.
```

**Acciones:**
- Ejecutar `npm test`
- Mostrar que todos pasan
- Explicar qué está probando cada property

**Checkpoint:** Property tests implementados y pasando

---

### Minutos 95-100: Configurar Agent Hook

**Guía:** [HOOKS-GUIDE.md](features/HOOKS-GUIDE.md)

**Script sugerido:**
```
"Ahora vamos a automatizar la ejecución de tests.
Cada vez que guardemos un archivo, los tests se ejecutarán automáticamente."
```

**Acciones:**
1. Abrir panel de Agent Hooks en Kiro
2. Crear nuevo hook:
   - Nombre: "Ejecutar tests al guardar"
   - Trigger: onFileSave
   - Pattern: `**/*.ts`
   - Command: `npm test`
3. Guardar y activar

**Demostración:**
- Modificar un archivo .ts
- Guardar
- Mostrar que tests se ejecutan automáticamente

**Checkpoint:** Hook configurado y funcionando

---

### Minutos 100-105: Configurar MCP Server (Opcional)

**Guía:** [MCP-GUIDE.md](features/MCP-GUIDE.md)

**Script sugerido:**
```
"MCP servers extienden las capacidades de Kiro.
Vamos a configurar el servidor filesystem como ejemplo."
```

**Acciones:**
1. Crear `.kiro/settings/mcp.json`
2. Configurar servidor filesystem
3. Verificar conexión

**Prompt de prueba:**
```
Usando herramientas MCP, lista los archivos en examples/spec/
```

**Nota:** Esta sección es opcional si el tiempo es limitado.

---

### Minutos 105-115: GitHub y CI/CD

**Guía:** [GITHUB-CICD-GUIDE.md](features/GITHUB-CICD-GUIDE.md)

**Script sugerido:**
```
"Ahora vamos a integrar con GitHub y configurar CI/CD
para que los tests se ejecuten automáticamente en cada push."
```

#### Minutos 105-107: Inicializar Git

**Comandos:**
```bash
git init
git add .
git commit -m "Initial commit: Validador de actas"
```

#### Minutos 107-110: Crear Workflow de GitHub Actions

**Prompt:**
```
Crea .github/workflows/ci.yml que:
- Se ejecute en push y PR a main
- Use Node.js 20
- Instale dependencias con npm ci
- Ejecute tests con npm test
```

#### Minutos 110-115: Push y Verificar

**Acciones:**
- Crear repositorio en GitHub
- Push del código
- Mostrar workflow ejecutándose
- Verificar que tests pasan

**Checkpoint:** CI/CD configurado y funcionando

---

### Minutos 115-120: Q&A y Cierre

**Script sugerido:**
```
"Hemos cubierto mucho en 2 horas:
- Modo Vibe para desarrollo rápido
- Modo Spec para desarrollo estructurado
- Property-based testing para correctitud
- Steering files, hooks y MCP para automatización
- GitHub y CI/CD para integración continua

¿Preguntas?"
```

**Recursos para compartir:**
- Link al repositorio
- FAQ.md para consulta
- Guías específicas para profundizar
- Comunidad de Kiro

**Siguiente pasos sugeridos:**
1. Experimentar con proyectos propios
2. Crear specs para funcionalidades reales
3. Explorar características avanzadas
4. Compartir experiencia con el equipo

---

## 🎭 Tips para el Instructor

### Manejo del Tiempo

**Si vas adelantado:**
- Profundiza en property-based testing
- Muestra más ejemplos de prompts
- Demuestra características avanzadas
- Responde más preguntas

**Si vas atrasado:**
- Salta la configuración de MCP (opcional)
- Reduce tiempo de Q&A intermedio
- Combina pasos similares
- Enfócate en conceptos clave

### Manejo de Errores

**Si Kiro genera código incorrecto:**
- Mantén la calma, es parte del aprendizaje
- Muestra cómo pedir correcciones específicas
- Usa #Problems para dar contexto
- Explica que revisar código es importante

**Si los tests fallan:**
- Revisa el error con los participantes
- Muestra cómo debuggear con Kiro
- Usa como oportunidad de aprendizaje
- Ten código de backup si es crítico

**Si hay problemas técnicos:**
- Ten capturas de pantalla de resultados esperados
- Usa código pre-generado como backup
- Continúa con la explicación conceptual
- Ofrece ayuda individual después

### Engagement

**Mantén participación:**
- Haz preguntas frecuentes
- Pide que compartan pantalla
- Verifica comprensión regularmente
- Usa ejemplos del contexto electoral

**Señales de confusión:**
- Caras confundidas → Pausa y explica de nuevo
- Silencio prolongado → Haz preguntas directas
- Muchas preguntas básicas → Reduce velocidad
- Pocos siguiendo → Verifica entorno técnico

---

## 📊 Métricas de Éxito

Al final de la demo, los participantes deberían poder:

- [ ] Explicar diferencia entre Vibe y Spec
- [ ] Crear un spec básico (requirements, design, tasks)
- [ ] Usar #File, #Folder, #Codebase
- [ ] Configurar un steering file
- [ ] Configurar un agent hook
- [ ] Entender property-based testing
- [ ] Optimizar consumo de tokens

---

## 📝 Checklist Post-Demo

**Inmediatamente después:**
- [ ] Compartir link al repositorio
- [ ] Enviar FAQ y recursos adicionales
- [ ] Recopilar feedback de participantes
- [ ] Anotar mejoras para próxima demo

**Seguimiento:**
- [ ] Responder preguntas pendientes
- [ ] Compartir grabación (si aplica)
- [ ] Ofrecer sesión de Q&A adicional
- [ ] Crear canal de comunicación para dudas

---

## 🔗 Referencias Rápidas

### Guías por Tema

| Tema | Guía | Duración |
|------|------|----------|
| Proyecto Vibe | [VIBE-GUIDE.md](projects/VIBE-GUIDE.md) | 15 min |
| Formato EARS | [EARS-GUIDE.md](projects/EARS-GUIDE.md) | 5 min |
| Proyecto Spec | [SPEC-GUIDE.md](projects/SPEC-GUIDE.md) | ~90 min |
| Steering Files | [STEERING-GUIDE.md](features/STEERING-GUIDE.md) | 5-10 min |
| Agent Hooks | [HOOKS-GUIDE.md](features/HOOKS-GUIDE.md) | 5-10 min |
| MCP Servers | [MCP-GUIDE.md](features/MCP-GUIDE.md) | 10-15 min |
| GitHub/CI/CD | [GITHUB-CICD-GUIDE.md](features/GITHUB-CICD-GUIDE.md) | 10 min |
| Mejores Prácticas | [BEST-PRACTICES.md](best-practices/BEST-PRACTICES.md) | Referencia |
| Avanzado | [ADVANCED-FEATURES.md](best-practices/ADVANCED-FEATURES.md) | Referencia |

### Prompts Clave

**Setup:**
```
Crea un proyecto Node.js con TypeScript, Vitest y fast-check
```

**Types:**
```
Usando #File design.md, crea las interfaces según el diseño
```

**Parser:**
```
Usando #File design.md, implementa ActaParser con manejo de errores en español
```

**Validator:**
```
Usando #File design.md, implementa ActaValidator con las tres validaciones
```

**Property Tests:**
```
Crea property tests con fast-check para las correctness properties del design
```

---

**¡Éxito en tu demo!** 🚀
