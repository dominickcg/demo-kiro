# Guía de GitHub y CI/CD

**Duración:** 10 minutos  
**Objetivo:** Configurar repositorio Git y CI/CD con GitHub Actions para validación automática

## Introducción

Esta guía te muestra cómo integrar tu proyecto de Kiro con GitHub y configurar CI/CD para ejecutar tests automáticamente en cada push o pull request.

**Beneficios:**
- ✅ Validación automática de código
- ✅ Detectar errores antes de merge
- ✅ Mantener calidad del código
- ✅ Documentar estado del proyecto (badges)

---

## Fase 1: Inicializar Repositorio Git (2 minutos)

### Paso 1.1: Inicializar Git

**Comando:**
```bash
git init
```

**Resultado:** Crea repositorio Git local en tu proyecto.

### Paso 1.2: Crear .gitignore

**Prompt para Kiro:**
```
Crea un archivo .gitignore para un proyecto Node.js con TypeScript que incluya:
- node_modules/
- dist/
- build/
- .env
- *.log
- coverage/
```

**Verificar:** El archivo `.gitignore` existe en la raíz del proyecto.

### Paso 1.3: Primer Commit

**Comandos:**
```bash
git add .
git commit -m "Initial commit: Validador de actas electorales"
```

**Resultado:** Código inicial commiteado al repositorio local.

---

## Fase 2: Crear Repositorio en GitHub (2 minutos)

### Paso 2.1: Crear Repositorio

**Opciones:**

**Opción A: Desde GitHub Web**
1. Ve a https://github.com
2. Haz clic en "New repository"
3. Nombre: `validador-actas-electorales`
4. Descripción: "Validador de actas electorales con property-based testing"
5. Público o Privado (tu elección)
6. NO inicialices con README (ya tienes código)
7. Haz clic en "Create repository"

**Opción B: Desde GitHub CLI**
```bash
gh repo create validador-actas-electorales --public --source=. --remote=origin
```

### Paso 2.2: Conectar Repositorio Local

**Comandos (si usaste Opción A):**
```bash
git remote add origin https://github.com/TU-USUARIO/validador-actas-electorales.git
git branch -M main
git push -u origin main
```

**Resultado:** Código subido a GitHub.

---

## Fase 3: Configurar GitHub Actions (4 minutos)

### Paso 3.1: Crear Workflow de CI

**Prompt para Kiro:**
```
Crea un workflow de GitHub Actions en .github/workflows/ci.yml que:
1. Se ejecute en push y pull_request a la rama main
2. Use Node.js versión 20
3. Instale dependencias con npm ci
4. Ejecute los tests con npm test
5. Ejecute el linter si existe
6. Funcione en ubuntu-latest
```

**Archivo esperado:** `.github/workflows/ci.yml`

### Paso 3.2: Contenido del Workflow

**Ejemplo completo:**

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [20.x]
    
    steps:
    - name: Checkout código
      uses: actions/checkout@v4
    
    - name: Configurar Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    
    - name: Instalar dependencias
      run: npm ci
    
    - name: Ejecutar linter
      run: npm run lint --if-present
    
    - name: Ejecutar tests
      run: npm test
    
    - name: Generar reporte de cobertura
      run: npm run test:coverage --if-present
```

### Paso 3.3: Commit y Push del Workflow

**Comandos:**
```bash
git add .github/workflows/ci.yml
git commit -m "Add CI workflow with GitHub Actions"
git push
```

**Resultado:** Workflow configurado y subido a GitHub.

---

## Fase 4: Verificar CI/CD (2 minutos)

### Paso 4.1: Ver Ejecución del Workflow

1. Ve a tu repositorio en GitHub
2. Haz clic en la pestaña "Actions"
3. Verás el workflow "CI" ejecutándose
4. Haz clic en la ejecución para ver detalles

### Paso 4.2: Verificar Resultados

**Resultado esperado:**
- ✅ Checkout código
- ✅ Configurar Node.js
- ✅ Instalar dependencias
- ✅ Ejecutar linter (si existe)
- ✅ Ejecutar tests

**Si todo pasa:** ✓ Workflow exitoso (verde)  
**Si algo falla:** ✗ Workflow fallido (rojo)

### Paso 4.3: Revisar Logs

Si el workflow falla:
1. Haz clic en el paso que falló
2. Lee el log de error
3. Corrige el problema localmente
4. Commit y push de nuevo

---

## Configuraciones Adicionales

### Agregar Badge de Estado

**Paso 1: Obtener Badge**
1. Ve a Actions en GitHub
2. Haz clic en el workflow "CI"
3. Haz clic en "..." → "Create status badge"
4. Copia el markdown

**Paso 2: Agregar a README**

**Prompt para Kiro:**
```
Agrega este badge al inicio del README.md:
[pegar el markdown del badge]
```

**Resultado:** Badge visible en el README mostrando estado del CI.

### Ejecutar Tests en Múltiples Versiones de Node

**Modificar workflow:**

```yaml
strategy:
  matrix:
    node-version: [18.x, 20.x, 22.x]
```

**Resultado:** Tests se ejecutan en Node 18, 20 y 22.

### Agregar Reporte de Cobertura

**Paso 1: Configurar Vitest para Cobertura**

**Prompt para Kiro:**
```
Configura Vitest para generar reportes de cobertura y agrega el script test:coverage a package.json
```

**Paso 2: Modificar Workflow**

Agregar después de ejecutar tests:

```yaml
- name: Subir reporte de cobertura
  uses: codecov/codecov-action@v3
  with:
    files: ./coverage/coverage-final.json
```

---

## Workflow para Pull Requests

### Proteger Rama Main

**Configuración en GitHub:**

1. Ve a Settings → Branches
2. Haz clic en "Add rule"
3. Branch name pattern: `main`
4. Marca:
   - ✓ Require status checks to pass before merging
   - ✓ Require branches to be up to date before merging
   - Selecciona el check "test"
5. Guarda cambios

**Resultado:** No se puede hacer merge a main si los tests fallan.

### Flujo de Trabajo

1. Crear rama para feature: `git checkout -b feature/nueva-validacion`
2. Hacer cambios y commit
3. Push de la rama: `git push origin feature/nueva-validacion`
4. Crear Pull Request en GitHub
5. CI ejecuta tests automáticamente
6. Si pasan, puedes hacer merge
7. Si fallan, corrige y push de nuevo

---

## Comandos Útiles

### Git Básico

```bash
# Ver estado
git status

# Ver cambios
git diff

# Agregar archivos
git add .

# Commit
git commit -m "Mensaje descriptivo"

# Push
git push

# Pull (actualizar desde remoto)
git pull

# Ver historial
git log --oneline
```

### Ramas

```bash
# Crear rama
git checkout -b nombre-rama

# Cambiar de rama
git checkout nombre-rama

# Listar ramas
git branch

# Eliminar rama local
git branch -d nombre-rama

# Eliminar rama remota
git push origin --delete nombre-rama
```

### GitHub CLI

```bash
# Ver estado de checks
gh pr checks

# Ver PRs
gh pr list

# Crear PR
gh pr create

# Ver detalles de workflow
gh run list
gh run view [run-id]
```

---

## Ejemplo de Uso en la Demo

### Escenario: Agregar Nueva Validación

**Paso 1: Crear rama**
```bash
git checkout -b feature/validar-firmas
```

**Paso 2: Implementar validación**

**Prompt para Kiro:**
```
Agrega una nueva validación al ActaValidator que verifique que el acta tiene al menos 2 firmas de autoridades
```

**Paso 3: Escribir tests**

**Prompt para Kiro:**
```
Agrega tests para la nueva validación de firmas
```

**Paso 4: Commit y push**
```bash
git add .
git commit -m "Add signature validation"
git push origin feature/validar-firmas
```

**Paso 5: Crear PR**
```bash
gh pr create --title "Add signature validation" --body "Adds validation for minimum 2 signatures"
```

**Paso 6: Ver CI ejecutándose**
- Ve a GitHub → Pull Requests
- Observa que CI está ejecutando tests
- Espera a que termine

**Paso 7: Merge si pasa**
- Si tests pasan → Merge PR
- Si tests fallan → Corrige y push de nuevo

---

## Troubleshooting

### El workflow no se ejecuta

**Posibles causas:**
- Archivo en ubicación incorrecta (debe estar en `.github/workflows/`)
- Sintaxis YAML incorrecta
- Branch no coincide con el trigger

**Solución:**
1. Verifica la ubicación del archivo
2. Valida la sintaxis YAML (usa un validador online)
3. Revisa los triggers en el workflow

### Tests pasan localmente pero fallan en CI

**Posibles causas:**
- Dependencias faltantes en CI
- Variables de entorno diferentes
- Archivos no commiteados
- Diferencias de sistema operativo

**Solución:**
1. Verifica que todas las dependencias están en package.json
2. Revisa los logs del CI para ver el error específico
3. Asegúrate de que todos los archivos necesarios están commiteados
4. Prueba localmente con `npm ci` en lugar de `npm install`

### Workflow muy lento

**Posibles causas:**
- Instalación de dependencias lenta
- Tests muy lentos
- Sin caché de dependencias

**Solución:**
1. Usa `cache: 'npm'` en setup-node
2. Optimiza tests lentos
3. Considera ejecutar solo tests relevantes en PR

---

## Mejores Prácticas

### ✅ Hacer

- Ejecutar tests localmente antes de push
- Escribir mensajes de commit descriptivos
- Crear PRs pequeños y enfocados
- Revisar logs de CI cuando fallan
- Mantener workflow actualizado

### ❌ Evitar

- Push directo a main sin tests
- Commits con mensajes vagos ("fix", "update")
- PRs muy grandes con muchos cambios
- Ignorar fallos de CI
- Deshabilitar checks para hacer merge rápido

---

## Recursos Adicionales

- **GitHub Actions Docs:** https://docs.github.com/actions
- **GitHub CLI:** https://cli.github.com
- **Git Docs:** https://git-scm.com/doc
- **Conventional Commits:** https://www.conventionalcommits.org

---

## Siguiente Paso

Ahora que tienes CI/CD configurado:
1. Todos los cambios se validan automáticamente
2. Puedes trabajar con confianza sabiendo que los tests se ejecutan
3. El equipo puede colaborar con PRs protegidos por CI

**Archivos relacionados:**
- `BEST-PRACTICES.md` - Mejores prácticas de desarrollo
- `ADVANCED-FEATURES.md` - Características avanzadas de Kiro
