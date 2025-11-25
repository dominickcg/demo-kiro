# Mejores Prácticas de Kiro

Esta guía te ayudará a usar Kiro de manera eficiente, optimizando tu productividad y consumo de tokens.

---

## 1. Uso de Contexto: #File, #Folder, #Codebase, #Problems

### #File - Incluir Archivos Específicos

**Cuándo usar:**
- Cuando necesitas que Kiro vea el contenido de un archivo específico
- Para modificar o refactorizar código existente
- Para generar código relacionado con un archivo

**Ejemplo:**
```
Usando #File src/validator/actaValidator.ts

Agrega una nueva validación que verifique que el acta tiene fecha válida
```

**Ventajas:**
- ✅ Kiro ve el contexto exacto
- ✅ Genera código consistente con el existente
- ✅ Más preciso que describir el archivo

**Evitar:**
- ❌ Incluir archivos muy grandes innecesariamente
- ❌ Incluir múltiples archivos cuando solo necesitas uno
- ❌ Pegar código manualmente en lugar de usar #File

---

### #Folder - Incluir Carpetas Completas

**Cuándo usar:**
- Cuando trabajas con múltiples archivos relacionados
- Para refactorizar una carpeta completa
- Para entender la estructura de un módulo

**Ejemplo:**
```
Usando #Folder src/validator/

Refactoriza el código para usar un patrón de strategy para las validaciones
```

**Ventajas:**
- ✅ Kiro ve toda la estructura del módulo
- ✅ Útil para refactorings grandes
- ✅ Mantiene consistencia entre archivos relacionados

**Evitar:**
- ❌ Incluir carpetas muy grandes (muchos archivos)
- ❌ Incluir carpetas con archivos no relacionados
- ❌ Usar cuando solo necesitas un archivo específico

---

### #Codebase - Buscar en Todo el Proyecto

**Cuándo usar:**
- Para encontrar dónde se usa una función o clase
- Para entender cómo se implementa algo en el proyecto
- Para buscar patrones o ejemplos existentes

**Ejemplo:**
```
Usando #Codebase busca todos los lugares donde se usa ActaValidator
```

**Ventajas:**
- ✅ Búsqueda en todo el proyecto
- ✅ Encuentra patrones y ejemplos
- ✅ Útil para entender código desconocido

**Evitar:**
- ❌ Usar para búsquedas muy amplias o vagas
- ❌ Usar cuando ya sabes dónde está el código
- ❌ Búsquedas que retornan demasiados resultados

**Tip:** Sé específico en tu búsqueda para obtener mejores resultados.

---

### #Problems - Ver Errores y Advertencias

**Cuándo usar:**
- Cuando tienes errores de compilación
- Para ver advertencias del linter
- Para que Kiro entienda qué está fallando

**Ejemplo:**
```
Usando #Problems

Corrige los errores de TypeScript en el proyecto
```

**Ventajas:**
- ✅ Kiro ve exactamente qué está fallando
- ✅ Puede sugerir correcciones específicas
- ✅ Más eficiente que describir los errores

**Evitar:**
- ❌ Usar cuando no hay errores
- ❌ Ignorar los errores y seguir desarrollando

---

## 2. Dividir Tareas Complejas en Pasos Pequeños

### ❌ Mal Enfoque: Todo de una vez

```
Crea una aplicación completa de validación de actas con parser, validator, 
CLI, tests, documentación, y deploy a producción
```

**Problemas:**
- Resultado impredecible
- Difícil de revisar
- Consume muchos tokens
- Errores difíciles de detectar

### ✅ Buen Enfoque: Paso a paso

**Paso 1:**
```
Crea las interfaces TypeScript para Acta, VoteTally y ValidationResult
```

**Paso 2:**
```
Implementa ActaParser que lea y parsee archivos JSON de actas
```

**Paso 3:**
```
Implementa ActaValidator con las tres validaciones principales
```

**Paso 4:**
```
Crea la interfaz CLI que use el parser y validator
```

**Paso 5:**
```
Escribe tests unitarios para el validator
```

**Ventajas:**
- ✅ Resultados predecibles
- ✅ Fácil de revisar cada paso
- ✅ Detectas errores temprano
- ✅ Puedes ajustar el rumbo si es necesario

---

## 3. Optimización de Consumo de Tokens

### Estrategias para Ahorrar Tokens

#### 1. Usa #File en lugar de pegar código

**❌ Consume más tokens:**
```
Tengo este código:
[pegar 200 líneas de código]

Agrega una función que...
```

**✅ Consume menos tokens:**
```
Usando #File src/validator.ts

Agrega una función que...
```

#### 2. Sé específico y conciso

**❌ Vago y largo:**
```
Necesito que me ayudes a crear algo que valide actas electorales, 
no estoy seguro exactamente qué necesito pero básicamente quiero 
que revise si los números están bien y que no haya errores...
```

**✅ Específico y conciso:**
```
Crea una función validateActa que verifique:
1. Suma de votos = total declarado
2. No hay votos negativos
3. Total no excede votantes habilitados
```

#### 3. Usa Steering Files para convenciones

**❌ Repetir en cada prompt:**
```
Crea una función en camelCase, con comentarios en español, 
que use interfaces en lugar de types, y que...
```

**✅ Definir una vez en steering file:**
```
Crea una función que calcule el porcentaje de participación
```

(Kiro usa automáticamente las convenciones del steering file)

#### 4. Divide sesiones por contexto

En lugar de una sesión gigante con todo el proyecto:
- Sesión 1: Implementar parser
- Sesión 2: Implementar validator
- Sesión 3: Implementar CLI
- Sesión 4: Escribir tests

**Ventaja:** Cada sesión tiene solo el contexto necesario.

---

### Monitorear Consumo de Tokens

**Dónde ver:**
- Después de cada respuesta de Kiro
- En el panel de usuario (consumo acumulado)

**Qué revisar:**
- Tokens por mensaje
- Tendencias de consumo
- Comparar diferentes enfoques

**Tip:** Si un prompt consume muchos tokens, considera dividirlo en pasos más pequeños.

---

## 4. Ejemplos de Buenos y Malos Prompts

### Ejemplo 1: Crear una Función

**❌ Mal prompt:**
```
haz una funcion
```

**Problemas:**
- No especifica qué hace la función
- No indica lenguaje o contexto
- No menciona parámetros o retorno

**✅ Buen prompt:**
```
Crea una función validateSumConsistency en TypeScript que:
- Reciba un objeto Acta
- Verifique que la suma de votos individuales = totalVotos
- Retorne string con error o null si es válida
- Use el formato de error del design document
```

---

### Ejemplo 2: Refactorizar Código

**❌ Mal prompt:**
```
mejora este codigo
```

**Problemas:**
- No especifica qué mejorar
- "Mejorar" es subjetivo
- No da contexto

**✅ Buen prompt:**
```
Usando #File src/validator.ts

Refactoriza el método validate para:
1. Extraer cada validación a un método privado
2. Acumular errores en un array
3. Retornar ValidationResult con todos los errores
```

---

### Ejemplo 3: Corregir Errores

**❌ Mal prompt:**
```
no funciona, arreglalo
```

**Problemas:**
- No especifica qué no funciona
- No incluye el error
- No da contexto

**✅ Buen prompt:**
```
Usando #File src/parser.ts y #Problems

El parser está fallando con este error:
"Cannot read property 'votosPorCandidato' of undefined"

Corrige el manejo de casos donde el JSON no tiene el campo votosPorCandidato
```

---

### Ejemplo 4: Escribir Tests

**❌ Mal prompt:**
```
escribe tests
```

**Problemas:**
- No especifica qué testear
- No indica framework
- No menciona casos específicos

**✅ Buen prompt:**
```
Usando #File src/validator.ts

Crea tests unitarios con Vitest para ActaValidator que verifiquen:
1. Acta válida pasa validación
2. Acta con suma incorrecta falla
3. Acta con voto negativo falla
4. Acta con total > habilitados falla

Usa los archivos de examples/spec/ como datos de prueba
```

---

## 5. Patrones de Prompts Efectivos

### Patrón 1: Contexto + Acción + Criterios

```
Usando #File [archivo]

[Acción específica] que:
1. [Criterio 1]
2. [Criterio 2]
3. [Criterio 3]
```

**Ejemplo:**
```
Usando #File src/types/acta.ts

Agrega una nueva interface ValidationError que:
1. Tenga campo code (string)
2. Tenga campo message (string)
3. Tenga campo field opcional (string)
```

---

### Patrón 2: Problema + Contexto + Solución Esperada

```
[Descripción del problema]

Usando #File [archivo] y #Problems

[Solución esperada]
```

**Ejemplo:**
```
Los tests están fallando porque ActaParser no maneja archivos vacíos

Usando #File src/parser.ts y #Problems

Agrega validación que lance error descriptivo cuando el archivo está vacío
```

---

### Patrón 3: Referencia + Implementación

```
Usando #File [archivo de referencia]

Implementa [componente nuevo] siguiendo el mismo patrón que [referencia]
```

**Ejemplo:**
```
Usando #File src/validator/actaValidator.ts

Implementa DocumentValidator siguiendo el mismo patrón de validación que ActaValidator
```

---

## 6. Trabajo con Specs

### Flujo Recomendado

1. **Crear Requirements**
   - Define qué necesitas construir
   - Usa formato EARS
   - Sé específico en acceptance criteria

2. **Crear Design**
   - Define arquitectura
   - Especifica interfaces
   - Define correctness properties

3. **Crear Tasks**
   - Divide en pasos implementables
   - Referencia requirements
   - Incluye checkpoints

4. **Ejecutar Tasks**
   - Una tarea a la vez
   - Verifica cada paso
   - Ajusta si es necesario

### Prompts para Specs

**Crear spec:**
```
Crea un spec para [funcionalidad] que incluya requirements, design y tasks
```

**Actualizar spec:**
```
Actualiza el design del spec [nombre] para incluir [nueva funcionalidad]
```

**Ejecutar tarea:**
```
Ejecuta la tarea 3.1 del spec [nombre]
```

---

## 7. Mejores Prácticas Generales

### ✅ Hacer

- **Ser específico:** Describe exactamente qué necesitas
- **Dar contexto:** Usa #File, #Folder cuando sea relevante
- **Dividir tareas:** Pasos pequeños son más manejables
- **Verificar resultados:** Revisa el código generado
- **Iterar:** Pide ajustes si algo no está perfecto
- **Usar steering files:** Define convenciones una vez
- **Monitorear tokens:** Revisa tu consumo regularmente
- **Aprovechar specs:** Para proyectos estructurados

### ❌ Evitar

- **Prompts vagos:** "haz algo", "mejora esto"
- **Todo de una vez:** Tareas muy grandes
- **Pegar código:** Usa #File en su lugar
- **Ignorar errores:** Usa #Problems para contexto
- **Repetir convenciones:** Usa steering files
- **Sesiones infinitas:** Divide por contexto
- **No revisar:** Siempre verifica el código generado

---

## 8. Troubleshooting

### Kiro no entiende lo que necesito

**Solución:**
1. Sé más específico en tu prompt
2. Proporciona ejemplos
3. Usa #File para dar contexto
4. Divide la tarea en pasos más pequeños

### El código generado no es correcto

**Solución:**
1. Revisa si el prompt fue claro
2. Proporciona más contexto con #File
3. Pide correcciones específicas
4. Usa #Problems para mostrar errores

### Consumo alto de tokens

**Solución:**
1. Usa #File en lugar de pegar código
2. Sé más conciso en tus prompts
3. Divide en sesiones más pequeñas
4. Usa steering files para convenciones

### Resultados inconsistentes

**Solución:**
1. Usa steering files para mantener consistencia
2. Referencia archivos existentes como ejemplos
3. Sé más específico en los criterios
4. Usa specs para proyectos estructurados

---

## 9. Checklist de Prompt Efectivo

Antes de enviar un prompt, verifica:

- [ ] ¿Es específico y claro?
- [ ] ¿Incluye contexto necesario (#File, #Folder)?
- [ ] ¿Define criterios de éxito?
- [ ] ¿Es una tarea manejable (no muy grande)?
- [ ] ¿Usa terminología consistente?
- [ ] ¿Referencia documentación relevante (specs, design)?

---

## 10. Recursos Adicionales

- **EARS-GUIDE.md:** Formato de requirements
- **SPEC-GUIDE.md:** Desarrollo estructurado
- **STEERING-GUIDE.md:** Configurar convenciones
- **HOOKS-GUIDE.md:** Automatizar tareas
- **MCP-GUIDE.md:** Extender capacidades
- **FAQ.md:** Preguntas frecuentes

---

## Conclusión

Usar Kiro efectivamente es una habilidad que se desarrolla con práctica. Estas mejores prácticas te ayudarán a:

- ✅ Obtener mejores resultados
- ✅ Ahorrar tiempo y tokens
- ✅ Mantener código de calidad
- ✅ Trabajar de manera más eficiente

**Recuerda:** La clave es ser específico, dar contexto, y dividir tareas complejas en pasos manejables.
