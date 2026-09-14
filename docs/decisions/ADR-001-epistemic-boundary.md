# ADR-001 — Frontera epistemológica entre mundo, percepción y modelo interno

- **Estado:** aceptada
- **Fecha:** 2026-09-14
- **Versión:** 1.0
- **Alcance:** arquitectura experimental V1

## Contexto

El proyecto pretende estudiar cómo un sistema construye representaciones internas a partir de información parcial. Para medir esa construcción, el motor debe distinguir el estado real del entorno de las señales recibidas, las representaciones perceptivas y los patrones o modelos aprendidos.

`SUPUESTO` El simulador define un estado verdadero operacional. Esto no afirma que exista acceso filosóficamente neutral a la realidad; significa que, dentro del experimento, las reglas y variables del mundo son conocidas por el motor.

## Problema

Si el agente recibe posiciones, tipos, causalidad o etiquetas verdaderas, la arquitectura introduce como conocimiento aquello cuya inferencia se quiere investigar. Si además recibe identificadores técnicos, tick absoluto o glosas humanas, pueden aparecer capacidades espurias de temporalidad, identidad, categorización o agencia.

Se necesita una frontera auditable que permita comparar:

```text
GroundTruthState
vs. RawObservation
vs. PerceivedState
vs. PatternState
vs. InternalModel
```

## Decisión

`DECISIÓN DE ARQUITECTURA` El agente tendrá acceso a lo que percibe, nunca directamente a lo que realmente existe.

1. `GroundTruthState` será producido y leído únicamente por el motor y la instrumentación experimental.
2. Todo ingreso ambiental o corporal al agente atravesará sensores que produzcan `RawObservation`.
3. Las señales externas e internas permanecerán distinguibles por arquitectura en V1. Las internas describirán estado físico, no emoción, identidad o reacción.
4. `PerceivedState` podrá incluir primitivas estructuradas definidas por diseño, pero no semántica como amenaza, comida, enemigo, seguridad o miedo.
5. `PatternState` será el término preferido sobre `AbstractState` y contendrá patrones aprendidos sin etiquetas humanas.
6. Las interpretaciones humanas de patrones se guardarán fuera del estado accesible al agente.
7. La metadata experimental será un canal exclusivo del observador y no podrá condicionar decisiones ni aprendizaje.
8. El tick absoluto será metadata experimental. El agente podrá construir temporalidad solo desde secuencias, cambios y memoria.
9. La pertenencia corporal será conocida por el simulador para enrutar señales y acciones, pero no se entregará al agente como una afirmación de identidad ni como `continuity_id` cognitivo.
10. Las trazas deberán permitir auditar flujos y detectar filtraciones entre niveles.

## Alternativas consideradas

### Entregar el estado verdadero al agente

Rechazada para V1. Simplifica la implementación, pero elimina la diferencia entre realidad, observación e inferencia y hace imposible estudiar errores perceptivos o modelos divergentes.

### Entregar etiquetas semánticas predefinidas

Rechazada para el flujo cognitivo principal. Facilitaría la evaluación, pero programaría categorías humanas como “peligro”. Se permiten solo como anotaciones del observador.

### Entregar tick absoluto como entrada

Rechazada para V1. Proporcionaría artificialmente una variable temporal explícita y confundiría orden experimental con representación temporal aprendida.

### Entregar una identidad corporal persistente

Rechazada como dato cognitivo inicial. El simulador necesita una identidad técnica, pero exponerla preconfiguraría la continuidad y la frontera del yo.

### No definir Ground Truth

Rechazada para el mundo simulado V1. Impediría calcular errores sensoriales y contrastar representaciones. Puede reconsiderarse en entornos reales o parcialmente observables donde el estado verdadero no sea completamente accesible al investigador.

## Consecuencias positivas

- Permite medir separadamente error sensorial, transformación perceptiva, formación de patrones y error del modelo.
- Hace posibles experimentos controlados con ruido, oclusión y sensores heterogéneos.
- Reduce el riesgo de atribuir emergencia a información incorporada por diseño.
- Permite auditar las afirmaciones sobre temporalidad, agencia y autodistinción.
- Mantiene las etiquetas humanas como análisis externo y no como causas ocultas.

## Riesgos

- Las primitivas de `PerceivedState` pueden incorporar sesgos humanos aunque no usen etiquetas semánticas.
- Puede haber filtraciones indirectas por nombres de campos, orden estable, dimensiones, valores por defecto, recompensas, logs o configuración.
- Separar canales internos y externos ya introduce una frontera que el sistema no aprendió.
- Un Ground Truth simulado puede confundirse indebidamente con una afirmación ontológica general.
- La interpretación humana de patrones puede sobreajustarse retrospectivamente.

## Limitaciones

- La decisión garantiza separación informacional, no consciencia ni emergencia.
- No determina qué representación perceptiva mínima es adecuada.
- No demuestra que `PatternState` posea significado para el agente.
- No resuelve cómo medir experiencia fenomenal.
- No especifica todavía formatos serializados, algoritmos, ruido ni latencias.
- La frontera simulador/agente no reproduce necesariamente fronteras biológicas.

## Supuestos

- `SUPUESTO` Existe una separación arquitectónica inicial entre señales externas e internas.
- `SUPUESTO` El agente posee sensores.
- `SUPUESTO` Algunas primitivas perceptivas serán introducidas por diseño y documentadas.
- `SUPUESTO` No todo componente debe emerger.
- `SUPUESTO` El simulador define un `GroundTruthState` operacional.
- `SUPUESTO` El simulador conoce la frontera física agente/entorno.
- `SUPUESTO` Los canales de instrumentación pueden aislarse de los canales cognitivos.

## Implicaciones experimentales

Cada corrida deberá conservar vistas separadas y correlacionables por la instrumentación, no por el agente. Las pruebas de integración futuras deberán comprobar que campos prohibidos no atraviesan interfaces cognitivas.

`PREDICCIÓN` Con el mismo estado real, arquitectura y condición inicial, dos agentes con sensores distintos o diferente ruido pueden desarrollar `RawObservation`, `PerceivedState`, `PatternState`, modelos internos y respuestas divergentes.

`POSIBLE REFUTACIÓN` Si, tras múltiples réplicas y controles, las diferencias sensoriales definidas no producen las divergencias predichas, esa predicción particular quedará debilitada. Esto no probará ni refutará por sí solo la consciencia.

## Criterios para reconsiderar la decisión

Revisar este ADR si:

- una pregunta experimental requiere legítimamente acceso del agente a una variable global y se puede aislar como condición comparativa;
- se demuestra que una primitiva perceptiva filtra semántica o Ground Truth;
- no puede auditarse la ausencia de canales laterales;
- el proyecto migra a entornos donde el investigador tampoco conoce el estado verdadero completo;
- evidencia experimental obliga a cambiar la separación interno/externo;
- un protocolo necesita estudiar explícitamente el efecto de entregar tiempo, identidad o etiquetas, siempre como intervención y no como línea base.

Toda revisión debe crear un nuevo ADR o una nueva versión, preservar esta decisión, indicar evidencia o motivo y describir el impacto sobre la comparabilidad de experimentos.
