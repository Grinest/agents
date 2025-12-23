# Quick Start - Sync Claude Agents

## Uso Rápido

### Desde este repositorio

```bash
cd /ruta/a/claude-agents
./scripts/sync-agents.sh
```

### Con repositorio personalizado

```bash
# Opción 1: Como parámetro
./scripts/sync-agents.sh https://github.com/tu-empresa/company-agents.git

# Opción 2: Variable de entorno
AGENTS_REPO=https://github.com/tu-empresa/company-agents.git ./scripts/sync-agents.sh

# Opción 3: Exportar variable (permanente en la sesión)
export AGENTS_REPO="https://github.com/tu-empresa/company-agents.git"
./scripts/sync-agents.sh
```

### Desde cualquier proyecto (remoto)

```bash
# Con repositorio por defecto
curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh | bash

# Con repositorio personalizado
curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh | bash -s -- https://github.com/empresa/agents.git

# Crear alias permanente
echo 'alias sync-agents="bash -c \"\$(curl -sSL https://raw.githubusercontent.com/juanpaconpa/claude-agents/main/scripts/sync-agents.sh)\""' >> ~/.bashrc
source ~/.bashrc
```

## Ejemplos de Uso

### 1. Ver ayuda

```bash
./scripts/sync-agents.sh --help
```

### 2. Instalar todos los agentes

```bash
./scripts/sync-agents.sh
# Selecciona: [1]
```

### 3. Instalar agentes específicos

```bash
./scripts/sync-agents.sh
# Selecciona: [2]
# Ingresa: 1 3
# Esto instalará 'architect' y 'qa-backend-py'
```

### 4. Instalar rango de agentes

```bash
./scripts/sync-agents.sh
# Selecciona: [2]
# Ingresa: 1-2
# Esto instalará 'architect' y 'backend-py'
```

### 5. Usar repositorio de empresa

```bash
# Método directo
./scripts/sync-agents.sh https://github.com/mi-empresa/company-agents.git

# Con variable de entorno
AGENTS_REPO=https://github.com/mi-empresa/agents.git ./scripts/sync-agents.sh
```

## Agentes Disponibles

| # | Agente | Descripción |
|---|--------|-------------|
| 1 | architect | Especialista en arquitectura de software |
| 2 | backend-py | Desarrollo backend Python con Clean Architecture |
| 3 | qa-backend-py | Testing y QA para backend Python |

## Ubicación de Instalación

Los agentes se instalan en:
```
.claude/agents/
├── architect.md
├── backend-py.md
└── qa-backend-py.md
```

## Verificar Instalación

```bash
# Listar agentes instalados
ls -la .claude/agents/

# Ver agente instalado
cat .claude/agents/architect.md
```

## Actualizar Agentes

Simplemente ejecuta el script de nuevo y selecciona los agentes a actualizar. Los archivos existentes serán sobrescritos con la versión más reciente.

## Problemas Comunes

### Error: "No se pudo acceder a los agentes"
- Verifica tu conexión a internet
- Verifica que git esté instalado

### Error: "No se encontraron agentes disponibles"
- Verifica que estás en el directorio correcto
- Verifica que la carpeta `agents/` existe

### Los agentes no aparecen en Claude
- Reinicia Claude Code
- Verifica que los archivos estén en `.claude/agents/`
- Verifica que los archivos tengan el formato correcto

## Más Información

Para documentación completa, consulta [README.md](./README.md)