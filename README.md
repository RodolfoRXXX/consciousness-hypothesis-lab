# Consciousness Hypothesis Lab

Laboratorio de software para formular, implementar y poner a prueba una hipótesis modular sobre consciencia, construcción del yo, percepción, memoria, predicción y aprendizaje por experiencia.

## Propósito

El objetivo no es construir un sistema que *parezca* consciente ni demostrar de antemano que una hipótesis es correcta. El objetivo es construir un entorno experimental reproducible donde cada mecanismo propuesto pueda aislarse, modificarse o eliminarse, y donde las consecuencias de esas intervenciones puedan medirse.

## Principios

- **Modularidad:** cada pilar de la hipótesis se modela como un componente independiente.
- **Interpretabilidad:** la V1 prioriza mecanismos inspeccionables por encima de rendimiento o complejidad.
- **Falsabilidad:** cada experimento debe declarar qué resultado apoyaría, debilitaría o refutaría una hipótesis.
- **Reproducibilidad:** configuraciones, semillas, métricas y resultados deben quedar registrados.
- **Separación entre hipótesis y evidencia:** no se reinterpretan resultados para preservar la teoría.
- **Sin antropomorfización como criterio de prueba:** parecer humano no será evidencia suficiente de consciencia.

## Hipótesis de trabajo, versión inicial

La consciencia humana podría entenderse como una organización dinámica en la que un organismo integra señales presentes, estados internos, memoria, modelos aprendidos y predicciones para construir un mundo presente y un modelo persistente de sí mismo dentro de ese mundo. El "yo" no se asume como un observador separado, sino como una organización estable y autorreferencial de experiencias alrededor del mismo organismo.

Esta formulación es una hipótesis de trabajo, no una conclusión demostrada.

## Estructura

```text
consciousness-hypothesis-lab/
├── README.md
├── pyproject.toml
├── .gitignore
├── docs/
│   ├── PROJECT_REPORT_v0.1.docx
│   ├── decisions/
│   └── experiments/
├── src/consciousness_lab/
│   └── modules/
├── tests/
│   ├── unit/
│   └── integration/
├── experiments/
│   ├── protocols/
│   └── runs/
├── configs/
├── scripts/
├── data/
│   ├── raw/
│   └── processed/
└── notebooks/
```

## Módulos previstos

La primera arquitectura experimental contempla, como mínimo:

1. percepción;
2. abstracción;
3. memoria;
4. modelo del mundo;
5. predicción;
6. integración del presente;
7. modelo del yo;
8. valoración;
9. decisión/acción.

En la V1 estos módulos serán explícitos e interpretables. El aprendizaje estadístico o neuronal se incorporará de forma incremental solo después de establecer una línea base comprensible.

## Estrategia experimental

Cada ejecución deberá registrar:

- versión del código;
- configuración;
- semilla aleatoria;
- hipótesis evaluada;
- módulos activos/desactivados;
- condiciones del entorno;
- métricas predefinidas;
- resultados;
- interpretación y explicaciones alternativas.

El método principal será la **ablación modular**: comparar un agente completo contra variantes en las que se elimina o altera un único componente.

## Estado

**Fase 0 — Inicialización del proyecto.**

Todavía no hay implementación de los mecanismos. La prioridad actual es fijar estructura, documentación y contratos experimentales antes de comenzar a programar comportamiento.

## Documentación vigente

- [Informe principal v0.2](docs/PROJECT_REPORT.md)
- [ADR-001 — Frontera epistemológica](docs/decisions/ADR-001-epistemic-boundary.md)
- [Contratos conceptuales de datos](docs/data-contracts.md)
- [Glosario operativo](docs/glossary.md)

La versión 0.1 original del informe se conserva en `docs/PROJECT_REPORT_v0.1.docx`. El agente experimental no tendrá acceso directo al estado verdadero del entorno ni a metadata experimental; esta decisión no implementa todavía ningún módulo.
