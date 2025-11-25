# Guía del Ejercicio EARS - Formato de Requirements

**Duración:** 5 minutos  
**Objetivo:** Aprender a escribir requirements claros usando formato EARS con ayuda de Kiro

## ¿Qué es EARS?

EARS (Easy Approach to Requirements Syntax) es un método estructurado para escribir requirements sin ambigüedades. Kiro lo usa como estándar porque produce especificaciones claras y parseables.

## Los 6 Patrones EARS

### 1. Ubicuos (Ubiquitous)
Comportamientos siempre activos

**Formato:** `EL SISTEMA SHALL [comportamiento]`

**Ejemplo:**
```
EL SISTEMA SHALL encriptar todas las contraseñas usando bcrypt
```

### 2. Dirigidos por Eventos (Event-Driven)
Disparados por eventos específicos

**Formato:** `WHEN [evento] THEN EL SISTEMA SHALL [comportamiento]`

**Ejemplo:**
```
WHEN el usuario hace clic en logout THEN EL SISTEMA SHALL limpiar la sesión
```

### 3. Dirigidos por Estado (State-Driven)
Activos en un estado específico

**Formato:** `WHILE [estado] EL SISTEMA SHALL [comportamiento]`

**Ejemplo:**
```
WHILE un archivo se está subiendo EL SISTEMA SHALL mostrar barra de progreso
```

### 4. Características Opcionales (Optional)
Características que pueden incluirse

**Formato:** `WHERE [característica] EL SISTEMA SHALL [comportamiento]`

**Ejemplo:**
```
WHERE modo oscuro está habilitado EL SISTEMA SHALL usar tema oscuro
```

### 5. Comportamientos No Deseados (Unwanted)
Cosas que NO debe hacer

**Formato:** `EL SISTEMA SHALL NOT [comportamiento]`

**Ejemplo:**
```
EL SISTEMA SHALL NOT almacenar contraseñas en texto plano
```

### 6. Condiciones Complejas (Complex)
Múltiples condiciones

**Formato:** `WHEN [condición] AND [condición] THEN EL SISTEMA SHALL [comportamiento]`

**Ejemplo:**
```
WHEN usuario está autenticado AND tiene rol admin THEN EL SISTEMA SHALL mostrar panel de administración
```

---

## Ejercicio Práctico con Kiro

### Ejemplo 1: Requirement Vago

**Requirement mal escrito:**
```
El sistema debe validar actas rápido
```

**Prompt para Kiro:**
```
Convierte este requirement a formato EARS con criterios medibles:
"El sistema debe validar actas rápido"
```

**Respuesta esperada de Kiro:**
```
WHEN se valida un acta THEN el sistema SHALL completar la validación en menos de 2 segundos
```

**Aprendizaje:** EARS fuerza especificar "qué tan rápido" con un número medible.

### Ejemplo 2: Requirement Ambiguo

**Requirement mal escrito:**
```
El validador tiene que funcionar bien con archivos grandes
```

**Prompt para Kiro:**
```
Convierte este requirement a formato EARS con criterios específicos:
"El validador tiene que funcionar bien con archivos grandes"
```

**Respuesta esperada de Kiro:**
```
WHEN se procesa un archivo de acta de hasta 10MB THEN el sistema SHALL completar el procesamiento en menos de 5 segundos
```

**Aprendizaje:** EARS elimina términos vagos como "bien" y "grandes" con criterios específicos.

### Ejemplo 3: Requirement con Múltiples Condiciones

**Requirement mal escrito:**
```
Si hay errores en el acta, mostrarlos al usuario
```

**Prompt para Kiro:**
```
Convierte este requirement a formato EARS más específico:
"Si hay errores en el acta, mostrarlos al usuario"
```

**Respuesta esperada de Kiro:**
```
WHEN un acta es inválida THEN el sistema SHALL listar todos los errores encontrados con descripción específica de cada inconsistencia
```

**Aprendizaje:** EARS especifica exactamente QUÉ mostrar y CÓMO.

---

## Palabras a Evitar en EARS

| ❌ Evitar | ✅ Usar en su lugar |
|-----------|---------------------|
| Debería/Podría | SHALL (obligatorio) |
| Apropiado/Adecuado | Criterios específicos |
| Rápido/Lento | Tiempo en segundos/milisegundos |
| Grande/Pequeño | Tamaño en MB/KB o cantidad exacta |
| Amigable/Intuitivo | Métricas medibles de usabilidad |

---

## Práctica Adicional (Opcional)

Si tienes tiempo, practica convirtiendo estos requirements:

1. "La aplicación debe ser segura"
2. "El sistema tiene que manejar muchos usuarios"
3. "Los reportes deben generarse correctamente"

**Prompt para Kiro:**
```
Convierte estos 3 requirements a formato EARS con criterios medibles:
[pegar los 3 requirements]
```

---

## Siguiente Paso

Ahora que entiendes EARS, revisaremos los requirements del proyecto Spec que ya están escritos en formato EARS. Podrás identificar los patrones que acabas de aprender.

**Archivo a revisar:** `.kiro/specs/demo-task-manager/requirements.md`
