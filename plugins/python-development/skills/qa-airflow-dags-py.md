---
name: qa-airflow-dags-py
description: Estándares de testing para DAGs de Airflow, incluyendo arquitectura de tests de integración y unitarios.
model: sonnet
color: blue
---
# QA Airflow DAGs Skill

Estándares y procedimientos para asegurar la calidad en proyectos de Apache Airflow con Python, enfocados en la integridad de los DAGs y la validación de la lógica de transformación de datos.

## Tecnologías de Testing

- **Apache Airflow**: Para el contexto de ejecución y DagBag testing.
- **pytest**: Framework principal de pruebas.
- **unittest.mock**: Para el aislamiento de tareas y servicios externos.
- **pytest-mock**: Wrapper de pytest para mocking simplificado.

## Arquitectura de Pruebas

El repositorio de Airflow sigue una estructura de testing dividida entre integridad del flujo (integración) y lógica de negocio (unitaria).

### 1. Pruebas de Integración (Integridad de DAGs)

Validan que el DAG se cargue correctamente, no tenga ciclos y cumpla con los requerimientos de la plataforma (tags, owners, etc.).

- **Ubicación**: `tests/dags/{folder_dag_name}/test_{dag_id}.py`
- **Enfoque**: DagBag testing y validación de estructura.

### 2. Pruebas Unitarias (Lógica de Tareas)

Validan la lógica de transformación, extracción o carga contenida en scripts auxiliares o dentro de las tareas del DAG.

- **Ubicación**: `tests/scripts/python/{folder_dag_name}/[extraction | transformation | load]/{file_name}/test_{function_name}_from_{class_name}.py`
- **Reglas de Nomenclatura**:
  - Directorio: Espejo de la ubicación del script en `dags/` o `scripts/`.
  - Archivo: `test_{function_name}_from_{class_name}.py`.
  - Clase: `Test{FunctionName}From{ClassName}`.
  - Función: `test_should_{expected_behavior}_when_{condition}`.

## Patrones Recomendados

### DagBag Testing (Integración)
```python
from airflow.models import DagBag

def test_dag_loads_with_no_errors():
    dag_bag = DagBag(dag_folder="dags/", include_examples=False)
    assert not dag_bag.import_errors
```

### Unit Testing con Mocks
- Aislar las tareas de las conexiones reales a la base de datos o APIs externas.
- Validar que los parámetros pasados a los operadores/hooks sean los correctos.
- Probar el manejo de excepciones y reintentos.

## Requerimientos de Cobertura
- **Integridad**: 100% de los DAGs deben pasar el test de carga.
- **Lógica Crítica**: >90% de cobertura en scripts de transformación y extracción.
