# Quick Start Guide - Claude Agents & Workflows

Guía rápida para comenzar a usar agentes de Claude y workflows de GitHub Actions en tus proyectos usando el moderno sistema de plugins de Claude Code (2026).

## 🚀 Inicio Rápido

### Para Agentes y Skills (Método Moderno)

```bash
# 1. Agregar el marketplace
/plugin marketplace add Grinest/agents

# 2. Instalar plugins que necesites
/plugin install general@agents                # Arquitectura
/plugin install python-development@agents     # Python backend
/plugin install flutter-development@agents    # Flutter

# 3. Verificar instalación
/plugin list
```

### Para GitHub Workflows

```bash
# 1. Desde tu proyecto
cd /tu/proyecto

# 2. Ejecutar script de sincronización de workflows
/ruta/a/claude-agents/scripts/sync-workflows.sh

# 3. Seleccionar workflows deseados
# Opción 1: Todos los workflows
# Opción 2: Selección personalizada

# 4. Configurar secrets necesarios
# Ir a: GitHub Repo → Settings → Secrets → Actions
```

---

## 📦 Instalación Detallada

### Método 1: Plugin Marketplace (Recomendado) ⭐

El sistema de plugins es el método oficial de Claude Code 2026:

```bash
# Paso 1: Agregar marketplace
/plugin marketplace add Grinest/agents

# Paso 2: Ver plugins disponibles
/plugin marketplace browse claude-agents

# Paso 3: Instalar plugins
/plugin install general@agents
/plugin install python-development@agents
/plugin install flutter-development@agents
```

**Ventajas**:
- ✅ Instalación con un comando
- ✅ Actualizaciones automáticas disponibles
- ✅ Versionamiento semántico
- ✅ Sin necesidad de clonar repositorios
- ✅ Configuración de equipo centralizada

### Método 2: Configuración de Proyecto

Para que todo el equipo tenga los mismos plugins automáticamente:

```bash
# Crear configuración en tu proyecto
cat > .claude/settings.json << 'EOF'
{
  "plugin_marketplaces": ["Grinest/agents"],
  "plugins": [
    "general@agents",
    "python-development@agents",
    "flutter-development@agents"
  ]
}
EOF

# Commitear configuración
git add .claude/settings.json
git commit -m "Configure Claude Code plugins"
```

Los miembros del equipo obtienen plugins automáticamente al clonar el proyecto.

### Método 3: Instalación Manual (No Recomendado)

Si por alguna razón no puedes usar el sistema de plugins:

```bash
# Clonar repositorio
git clone https://github.com/Grinest/agents.git
cd claude-agents

# Copiar agentes manualmente
mkdir -p .claude/agents
cp plugins/general/agents/architect.md .claude/agents/
cp plugins/python-development/agents/backend-py.md .claude/agents/
cp plugins/python-development/skills/backend-py-celery.md .claude/agents/
```

> ⚠️ **Nota**: La instalación manual no tiene versionamiento ni auto-updates.

---

## 🎯 Uso de Agentes y Skills

### Ver Plugins Instalados

```bash
# Listar todos los plugins
/plugin list

# Ver detalles de un plugin
/plugin show python-development@agents

# Listar agentes disponibles
/agents list

# Listar skills disponibles
/skills list
```

### Usar Agentes

Los agentes se activan automáticamente según el contexto de tu solicitud:

```bash
# Arquitectura - activa el agente 'architect'
"Analiza la arquitectura de este proyecto y recomienda cómo implementar autenticación JWT"

# Backend Python - activa 'backend-py'
"Implementa un interactor para crear usuarios siguiendo Clean Architecture"

# QA Python - activa 'qa-backend-py'
"Escribe tests unitarios para este interactor con >90% de cobertura"
```

### Usar Skills

Los skills se invocan explícitamente con el prefijo `/`:

```bash
# Skill de desarrollo FastAPI + Celery
/backend-py-celery Create a new API endpoint for user authentication with JWT tokens

# Ver ayuda de un skill
/backend-py-celery --help

# Usar skill con namespace (si hay conflictos)
/python-development:backend-py-celery Create endpoint for logout
```

---

## 📋 Recursos Disponibles

### 🏗️ General Plugin

Agentes agnósticos de lenguaje para arquitectura y diseño.

| Agente | Descripción |
|--------|-------------|
| **architect** | Especialista en arquitectura de software y system design |

**Instalar**: `/plugin install general@agents`

---

### 🐍 Python Development Plugin

Agentes y skills para desarrollo backend Python con Clean Architecture.

| Recurso | Tipo | Descripción |
|---------|------|-------------|
| **backend-py** | Agente | Desarrollo backend con Clean Architecture |
| **qa-backend-py** | Agente | Testing y QA para backend Python |
| **reviewer-backend-py** | Agente | Code review automatizado de PRs |
| **reviewer-library-py** | Agente | Code review para librerías Python |
| **backend-py-celery** | Skill | Desarrollo de FastAPI routes y Celery tasks |

**Instalar**: `/plugin install python-development@agents`

---

### 📱 Flutter Development Plugin

Agentes para desarrollo de aplicaciones Flutter/Dart.

| Agente | Descripción |
|--------|-------------|
| **reviewer-flutter-app** | Code review automatizado para apps Flutter |

**Instalar**: `/plugin install flutter-development@agents`

---

## 📁 Estructura de Instalación

### Plugins (Sistema Moderno)

```
.claude/
└── plugins/
    └── claude-agents@juanpaconpa/
        ├── general/
        │   └── agents/
        │       └── architect.md
        ├── python-development/
        │   ├── agents/
        │   │   ├── backend-py.md
        │   │   ├── qa-backend-py.md
        │   │   └── reviewer-backend-py.md
        │   └── skills/
        │       └── backend-py-celery.md
        └── flutter-development/
            └── agents/
                └── reviewer-flutter-app.md
```

### Workflows (GitHub Actions)

```
tu-proyecto/
└── .github/
    └── workflows/
        └── code-review-backend-py.yml
```

---

## ✅ Verificar Instalación

### Verificar Plugins

```bash
# 1. Listar plugins instalados
/plugin list

# Deberías ver:
# ✓ general@agents (v1.0.0)
# ✓ python-development@agents (v1.0.0)
# ✓ flutter-development@agents (v1.0.0)

# 2. Verificar agentes disponibles
/agents list

# 3. Verificar skills disponibles
/skills list
```

### Verificar Workflows

```bash
# Listar workflows instalados
ls -la .github/workflows/

# Ver contenido del workflow
cat .github/workflows/code-review-backend-py.yml

# Verificar en GitHub
# Ve a: tu-repo → Actions → Verás los workflows disponibles
```

---

## ⚙️ Configuración Post-Instalación

### Para Agentes y Skills

No requiere configuración adicional - funcionan inmediatamente después de la instalación.

### Para Workflows

Después de instalar workflows, necesitas configurar:

#### 1. Secrets

```
GitHub Repo → Settings → Secrets and variables → Actions → New secret
```

Para `code-review-backend-py.yml`:
- `ANTHROPIC_API_KEY`: Tu API key de Anthropic

#### 2. Permisos

```
Settings → Actions → General → Workflow permissions
```

Selecciona:
- ✅ Read and write permissions
- ✅ Allow GitHub Actions to create and approve pull requests

#### 3. Probar Workflow

```bash
# Crear PR de prueba
git checkout -b test/workflow
echo "# Test" >> test.py
git add test.py
git commit -m "test: verify workflow"
git push origin test/workflow
gh pr create --title "Test Workflow" --body "Testing code review"
```

---

## 🔄 Actualizar Recursos

### Actualizar Plugins

```bash
# Actualizar un plugin específico
/plugin update python-development@agents

# Actualizar todos los plugins de un marketplace
/plugin update --marketplace claude-agents

# Ver versiones disponibles
/plugin show python-development@agents
```

### Actualizar Workflows

```bash
# Re-ejecuta el script de workflows
./scripts/sync-workflows.sh

# NOTA: Si personalizaste workflows, haz backup antes
cp .github/workflows/code-review-backend-py.yml .github/workflows/code-review-backend-py.yml.backup
```

---

## 🏢 Configuración para Equipos

### Opción A: Configuración de Proyecto (Recomendada)

Commitea la configuración al repositorio para que todos tengan los mismos plugins:

```json
// .claude/settings.json
{
  "plugin_marketplaces": ["Grinest/agents"],
  "plugins": [
    "general@agents",
    "python-development@agents"
  ]
}
```

```bash
git add .claude/settings.json
git commit -m "Configure Claude Code plugins for team"
git push
```

Todo el equipo obtiene automáticamente los plugins al clonar.

### Opción B: Marketplace Privado

Para empresas con agentes personalizados:

```bash
# 1. Fork este repositorio a tu organización
# GitHub: Fork Grinest/agents → empresa/claude-agents

# 2. Personaliza plugins
# Agrega tus agentes en plugins/company-standards/

# 3. Usa marketplace privado
/plugin marketplace add empresa/claude-agents
/plugin install company-standards@agents
```

### Opción C: Múltiples Marketplaces

Combina marketplace público con privado:

```json
// .claude/settings.json
{
  "plugin_marketplaces": [
    "Grinest/agents",    // Público
    "empresa/private-agents"         // Privado
  ],
  "plugins": [
    "python-development@agents",  // Público
    "company-standards@private-agents"   // Privado
  ]
}
```

---

## 🐛 Problemas Comunes

### Agentes

#### Los plugins no aparecen

```bash
# Verificar marketplaces configurados
/plugin marketplace list

# Verificar plugins instalados
/plugin list

# Reinstalar plugin
/plugin uninstall python-development@agents
/plugin install python-development@agents
```

#### Error al agregar marketplace

1. Verifica que el repositorio exista y sea público (o tengas acceso)
2. Verifica que contenga `.claude-plugin/marketplace.json`
3. Para repos privados, configura autenticación Git (SSH o tokens)

```bash
# Ver detalles del error
/plugin marketplace add owner/repo --verbose
```

#### Los agentes no se activan

1. Verifica que el plugin esté instalado: `/plugin list`
2. Los agentes se activan por contexto - prueba con solicitud específica
3. Para skills, usa el prefijo `/`: `/backend-py-celery --help`
4. Reinicia Claude Code si es necesario

### Workflows

#### Workflow no se ejecuta en PRs

1. Verifica que el workflow esté en `.github/workflows/`
2. Verifica que los paths coincidan con tu estructura
3. Verifica que GitHub Actions esté habilitado

#### Error: "Secret not found"

1. Ve a: Settings → Secrets → Actions
2. Verifica que `ANTHROPIC_API_KEY` esté configurado
3. El valor debe empezar con `sk-ant-`

#### Workflow falla con error de permisos

1. Ve a: Settings → Actions → General
2. Selecciona "Read and write permissions"
3. Habilita "Allow GitHub Actions to create and approve pull requests"

---

## 📚 Casos de Uso Comunes

### 1. Startup con Clean Architecture

```bash
# Instalar plugins necesarios
/plugin marketplace add Grinest/agents
/plugin install general@agents
/plugin install python-development@agents

# Instalar workflow de code review
./scripts/sync-workflows.sh  # Selecciona: code-review-backend-py

# Usar agentes en desarrollo
"Analiza este proyecto y recomienda cómo implementar autenticación"
"Implementa el sistema siguiendo Clean Architecture"
/backend-py-celery Create authentication endpoint with JWT
```

### 2. Empresa con repositorios privados

```bash
# Fork del repositorio a tu empresa
# GitHub: Fork → empresa/claude-agents

# Personalizar plugins
cd empresa/claude-agents
# Agregar plugins personalizados...

# Configurar en proyectos
# .claude/settings.json:
{
  "plugin_marketplaces": ["empresa/claude-agents"],
  "plugins": ["python-development@agents"]
}
```

### 3. Freelancer con múltiples clientes

```bash
# Proyecto Cliente A
cd ~/projects/cliente-a

# .claude/settings.json
{
  "plugin_marketplaces": ["cliente-a/agents"],
  "plugins": ["python-development@agents"]
}

# Proyecto Cliente B
cd ~/projects/cliente-b

# .claude/settings.json
{
  "plugin_marketplaces": ["cliente-b/agents"],
  "plugins": ["javascript-development@agents"]
}

# Los plugins se cargan automáticamente según el proyecto actual
```

---

## 🔗 Enlaces Útiles

### Documentación Principal

- [README del Proyecto](../README.md) - Documentación completa
- [Guía de Migración](../MIGRATION.md) - Migrar desde scripts bash
- [Plugin System](../.claude-plugin/README.md) - Sistema de plugins
- [Documentación de Scripts](../scripts/README.md) - Scripts de utilidad
- [Documentación de Workflows](../git-workflows/README.md) - GitHub Actions

### Documentación Específica

- [Arquitectura del Code Review Agent](./CODE_REVIEW_AGENT_ARCHITECTURE.md)
- [Guía de Despliegue CI/CD](./CI_CD_GUIDE_TO_CODE_REVIEW_AGENT.md)
- [Estrategia de Testing](./TESTING_STRATEGY.md)

### Recursos Externos

- [Claude Code Documentation](https://code.claude.com/docs)
- [Claude Code Plugins](https://code.claude.com/docs/en/plugins.md)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Anthropic API Documentation](https://docs.anthropic.com/api)

---

## 💡 Tips y Mejores Prácticas

### Para Plugins

1. **Configura en el proyecto**: Usa `.claude/settings.json` para que todo el equipo tenga los mismos plugins
2. **Mantén actualizados**: Ejecuta `/plugin update --marketplace claude-agents` regularmente
3. **Usa namespaces**: Si hay conflictos, usa `/plugin-name:skill-name`
4. **Versiona las configuraciones**: Commitea `.claude/settings.json` al repositorio
5. **Explora plugins**: Usa `/plugin marketplace browse` para descubrir nuevos recursos

### Para Workflows

1. **Prueba primero**: Usa branches de test para validar workflows antes de aplicarlos en main
2. **Monitorea costos**: Los workflows con Claude API tienen costo, revisa uso mensual
3. **Documenta personalizaciones**: Si modificas workflows, documenta los cambios
4. **Versionamiento**: Si haces cambios, considera guardar versiones anteriores
5. **Revisa logs**: Usa `gh run view <run-id> --log` para debugging

---

## 🆘 Soporte

¿Necesitas ayuda?

1. **Documentación**: Revisa la [documentación completa](../README.md)
2. **Migración**: Si vienes de scripts bash, lee [MIGRATION.md](../MIGRATION.md)
3. **Issues**: Busca en [issues existentes](https://github.com/Grinest/agents/issues)
4. **Nuevo issue**: Crea un [nuevo issue](https://github.com/Grinest/agents/issues/new) con:
   - Descripción del problema
   - Pasos para reproducir
   - Output de `/plugin list` y `/plugin show plugin-name`
   - Logs relevantes
   - Sistema operativo y versión de Claude Code

---

## 🎉 ¡Empezar es Fácil!

```bash
# En Claude Code, ejecuta:
/plugin marketplace add Grinest/agents
/plugin install python-development@agents

# ¡Listo! Ahora tienes agentes especializados disponibles
```

**¿Listo para empezar?** El sistema de plugins hace que usar agentes de Claude sea más fácil que nunca! 🚀
