# Proyecto experimental sobre consciencia

**Hipótesis modular, arquitectura documental y protocolo de validación**  
**Documento vivo — Versión 0.2 — 14 de septiembre de 2026**  
**Estado:** marco conceptual y diseño experimental inicial; no existen todavía resultados experimentales.

**Actualización de estado (2026-09-15):** el proyecto entró en una fase formal de [revisión del estado del arte](literature/state-of-the-art.md). La arquitectura propuesta hasta ahora es **PROVISIONAL — PENDIENTE DE REVISIÓN TEÓRICA**. Antes de la siguiente decisión se evaluará la secuencia `TEORÍA → INDICADORES → PREDICCIONES → ARQUITECTURA → EXPERIMENTO`; no se han congelado indicadores ni mecanismos adicionales y ADR-001 permanece aceptado.

**Refinamiento de misión (2026-09-15):** la [frontera entre herencia, aprendizaje, emergencia y metadata](development/inheritance-learning-emergence.md) pasa a ser una pregunta metodológica central. La arquitectura cognitiva permanece **PROVISIONAL — PENDIENTE DE REVISIÓN TEÓRICA Y EXPERIMENTAL**. Esta actualización amplía el foco de investigación sin borrar la hipótesis histórica ni modificar ADR-001.

Este documento es la versión Markdown mantenible del informe principal. La versión 0.1 original se conserva sin modificaciones en [`PROJECT_REPORT_v0.1.docx`](PROJECT_REPORT_v0.1.docx). Esta versión no reemplaza su historial: registra qué formulaciones se revisaron y por qué.

## 1. Propósito y alcance

`HIPÓTESIS` La consciencia podría ser una propiedad emergente de la organización dinámica mediante la cual un sistema integra percepción, abstracción, memoria, modelos internos, predicción, representación del presente, autorrepresentación, valoración y decisión.

No se postula una entidad separada llamada consciencia ni un observador interno adicional. Tampoco se afirma que implementar estos mecanismos sea suficiente para producir consciencia. El sistema será un modelo funcional, modular e interpretable destinado a producir predicciones contrastables y a admitir ablaciones, modificaciones y refutación.

El proyecto debe ser reproducible, inspeccionable, falsable y auditable. Un comportamiento que parezca humano, el uso de la palabra “yo” o una única ejecución llamativa no constituyen evidencia suficiente.

### 1.1 Misión refinada y objetivos

`OBJETIVO ACTUAL` El proyecto investiga hasta qué punto un agente artificial mínimo puede desarrollar, por experiencia e interacción con un entorno, capacidades cognitivas y patrones de comportamiento análogos a los de organismos conscientes. Partirá de una arquitectura inicial explícita y auditable para separar causalmente qué estructuras y conocimientos fueron heredados, qué contenidos se aprendieron y qué propiedades podrían considerarse emergentes. Reproducir comportamientos asociados con consciencia no implica experiencia fenomenal.

Esta misión ordena tres objetivos: **desarrollo cognitivo artificial** mediante historia individual y sin semántica humana precargada cuando sea experimentalmente posible; **descomposición causal** de la contribución de predisposiciones, condiciones, aprendizaje y diseño indirecto; **relación posterior con consciencia** mediante comparación con teorías e indicadores de la [revisión del estado del arte](literature/state-of-the-art.md). La consciencia continúa como motivación científica central, pero las capacidades funcionales, organizaciones candidatas y afirmaciones fenomenales se evalúan en niveles distintos.

La formulación de la sección 1 y las revisiones históricas de la sección 9 quedan como antecedentes de la hipótesis inicial, no como compromiso de implementar todos los módulos enumerados. Antes de V1 falta especificar `Agent(t0)`, procedencia de cada variable cognitiva, capacidad inicial, experiencia permitida, controles y falsadores; el [marco de procedencia](development/inheritance-learning-emergence.md) registra esas preguntas sin congelar nuevos módulos.

## 2. Frontera epistemológica

`DECISIÓN DE ARQUITECTURA` El agente debe tener acceso a lo que percibe, nunca directamente a lo que realmente existe.

El motor experimental y el investigador pueden conocer el estado verdadero y todas las transformaciones intermedias. El agente solo puede recibir señales de sensores y estados internos derivados de información autorizada. La decisión completa, sus alternativas y criterios de revisión están en [ADR-001](decisions/ADR-001-epistemic-boundary.md).

La separación mínima es:

```text
GroundTruthState  --sensores-->  RawObservation
                                      |
                                      v
                                PerceivedState
                                      |
                                      v
                                 PatternState
                                      |
                                      v
                                 InternalModel
```

El investigador puede comparar todos esos niveles. Ningún camino inverso ni canal lateral debe entregar `GroundTruthState` o metadata experimental al agente.

### 2.1 Nivel 1 — `GroundTruthState`

`DECISIÓN DE ARQUITECTURA` Es el estado real de la simulación, conocido por el motor: posiciones y tipos verdaderos, propiedades físicas, recursos, daño potencial, causalidad real, posición real del agente y perturbaciones externas. Es inaccesible para el agente.

```text
WorldObject:
    type = hazard
    position = (7, 3)
    damage = 0.5
```

El sensor puede producir señales afectadas por alcance, resolución y ruido, pero nunca entregar directamente `type = hazard`.

### 2.2 Nivel 2 — `RawObservation`

`DECISIÓN DE ARQUITECTURA` Contiene exclusivamente señales sensoriales.

- Las señales externas provienen del entorno: luz, distancia sensada, movimiento, temperatura externa, presión o señales espaciales.
- Las señales internas provienen del estado físico del cuerpo o sistema: temperatura interna, energía, integridad, daño sensado, posición relativa de partes o estado de actuadores.

Las señales internas son información sobre el estado físico interno, no “la reacción del sistema”. En este nivel no significan dolor, miedo, hambre, identidad ni emoción.

### 2.3 Nivel 3 — `PerceivedState`

`DECISIÓN DE ARQUITECTURA` Transforma señales crudas en propiedades estructuradas como dirección relativa, distancia percibida, tamaño, movimiento, cambio, intensidad, energía percibida o integridad percibida.

```text
RawObservation:
    sensor_1 = 0.83
    sensor_2 = 0.14

PerceivedState:
    entity_1:
        relative_direction = right
        distance = 0.18
        motion = 0.42
```

No puede introducir etiquetas como amenaza, comida, enemigo, seguridad o miedo. Incluso “objeto”, “entidad”, “distancia” y “movimiento” son primitivas elegidas por diseño; no deben reportarse como emergentes.

### 2.4 Nivel 4 — `PatternState`

`DECISIÓN DE ARQUITECTURA` `PatternState` reemplaza como término preferido a `AbstractState`. Representa patrones internos aprendidos a partir de recurrencias entre percepción, memoria y consecuencias, sin etiquetas humanas predefinidas.

```text
pattern_001 = 0.82
pattern_004 = 0.61
```

Un investigador podría observar que `pattern_001` se activa ante proximidad, movimiento rápido y una pérdida posterior de integridad, e interpretar que funciona de manera similar a una categoría de amenaza. Esa glosa humana no forma parte de la representación del agente y debe almacenarse como metadata o análisis externo.

## 3. Información del sistema y metadata experimental

`DECISIÓN DE ARQUITECTURA` La información accesible al sistema puede incluir lecturas sensoriales, estado corporal percibido, memoria, patrones y modelos aprendidos, predicciones, acciones propias registradas, consecuencias estimadas, estados internos, valores funcionales, incertidumbre y novedad.

`DECISIÓN DE ARQUITECTURA` Son exclusivos del observador: `run_id`, identificador técnico real del agente, tick absoluto, seed, escenario, versión del software, commit Git, módulos habilitados o deshabilitados, configuración experimental, estado verdadero del entorno, etiquetas humanas, posiciones absolutas reales y tipos verdaderos de objetos. Esta metadata no puede influir directa ni indirectamente en decisiones, aprendizaje o inicialización cognitiva del agente.

Los contratos y permisos por objeto se especifican en [Contratos de datos](data-contracts.md).

## 4. Tick y temporalidad

`DECISIÓN DE ARQUITECTURA` Un `tick` es una unidad discreta que ordena causal y temporalmente los ciclos del experimento; no representa necesariamente segundos reales.

```text
tick 41 -> estado previo
tick 42 -> percepción y decisión
tick 43 -> consecuencia y nueva observación
```

En V1 el tick absoluto existe solo como metadata experimental. El agente no recibe su número. Una representación temporal funcional futura deberá construirse a partir de secuencias, memoria, cambios y regularidades, no de un reloj global entregado por diseño.

## 5. Frontera yo / entorno

`SUPUESTO` El simulador conoce inicialmente qué cuerpo pertenece a cada agente y usa esa separación física para enrutar sensores y acciones.

`DECISIÓN DE ARQUITECTURA` El agente no recibe la afirmación “este cuerpo soy yo”. Un identificador como `continuity_id = agent_001` puede existir como metadata técnica, pero está prohibido como contenido cognitivo inicial de `SelfState`.

El agente puede acceder a señales internas y registros de sus acciones. Se estudiará si aprende correlaciones de la forma:

```text
acción registrada -> cambio corporal esperado
```

`PREGUNTA ABIERTA` ¿Puede esa regularidad sostener una distinción funcional entre cambios causados por el propio sistema y cambios causados externamente?

`POSIBLE REFUTACIÓN` Si la autodistinción solo aparece al introducir una etiqueta de identidad o una frontera propia explícita en el estado cognitivo, la afirmación de que surge de correlaciones sensorimotoras quedará debilitada o refutada para esa arquitectura.

## 6. Supuestos explícitos

Estas proposiciones son condiciones iniciales del modelo, no hipótesis confirmadas ni resultados:

- `SUPUESTO` Existe una separación arquitectónica entre señales externas e internas.
- `SUPUESTO` El sistema posee sensores con canales definidos por diseño.
- `SUPUESTO` Algunas propiedades perceptivas primitivas pueden estar predefinidas.
- `SUPUESTO` Ciertas estructuras de procesamiento son introducidas por diseño.
- `SUPUESTO` No todo elemento del sistema debe considerarse emergente.
- `SUPUESTO` El entorno simulado posee un `GroundTruthState` definido por los investigadores.
- `SUPUESTO` El simulador presupone inicialmente una separación física agente/entorno.

Convención documental:

- `HIPÓTESIS`: explicación que se someterá a contraste.
- `SUPUESTO`: condición aceptada para construir el modelo inicial.
- `DECISIÓN DE ARQUITECTURA`: restricción de diseño elegida.
- `PREGUNTA ABIERTA`: asunto aún no resuelto.
- `PREDICCIÓN`: consecuencia observable anticipada antes del experimento.
- `RESULTADO`: observación obtenida en un experimento ejecutado; por ahora no hay resultados.
- `POSIBLE REFUTACIÓN`: observación que debilitaría o invalidaría una afirmación especificada.
- `INTERPRETACIÓN`: lectura humana posterior que no debe confundirse con el estado del agente.

## 7. Implicación experimental: canales perceptivos distintos

`PREDICCIÓN` Dos agentes con igual arquitectura, entorno y situación inicial, pero con sensores diferentes o distinto ruido, pueden construir modelos internos y respuestas diferentes ante una misma realidad externa.

```text
mismo objeto real

Agente A: distance = 0.4, motion = 0.3
Agente B: distance = 0.7, motion = 0.8
```

La prueba deberá controlar arquitectura, estado inicial, entorno, política de intervención y seeds, variando solo el canal sensorial definido. Deberá comparar divergencias en `RawObservation`, `PerceivedState`, `PatternState`, modelo interno y decisiones.

`INTERPRETACIÓN` La relación “misma realidad externa ≠ misma representación interna” constituye una forma funcional y limitada de estudiar perspectiva o experiencia subjetiva. No constituye por sí sola prueba de consciencia.

## 8. Falsabilidad, ablación y trazabilidad

Cada protocolo deberá declarar previamente hipótesis, explicaciones alternativas, variables, controles, métricas y resultados que apoyarían, debilitarían o refutarían la afirmación. Las ablaciones deben conservar interfaces observables y evitar canales laterales de información. Los resultados negativos se preservarán.

Cada ejecución debe registrar, para el observador, versión documental y de software, commit, configuración, seed, escenario, módulos activos/inactivos, estado inicial, trazas epistemológicamente separadas, métricas, anomalías y exclusiones justificadas. Los cambios teóricos posteriores nunca se presentarán como predicciones previas.

## 9. Revisiones respecto de la versión 0.1

Las formulaciones anteriores permanecen en el `.docx` original. En la versión 0.2 se registran estas revisiones:

| Formulación 0.1 | Motivo de revisión | Formulación 0.2 |
|---|---|---|
| “Abstracción” convertía señales en rasgos o categorías y “amenaza” aparecía como propiedad tratable. | Podía introducir semántica humana antes del aprendizaje. | `PatternState` contiene patrones aprendidos sin etiquetas; cualquier equivalencia con “amenaza” es interpretación externa. |
| El modelo del yo “mantiene continuidad, estado propio y atribución de acciones”. | Podía codificar de antemano aquello cuya construcción se quiere estudiar. | `SelfState` no incluye identidad técnica ni una afirmación inicial de propiedad corporal; la atribución propia/externa es una capacidad a investigar. |
| El presente integrado combinaba “contexto temporal”. | No distinguía secuencias aprendibles del tick absoluto entregado por infraestructura. | El tick absoluto es metadata externa; la temporalidad del agente solo puede derivarse de secuencias, cambios y memoria. |
| Percepción se describía como captura de señales externas e internas. | No hacía explícita la barrera frente al estado verdadero. | Los sensores median todo acceso; `GroundTruthState` nunca es legible por el agente. |

Estas revisiones son decisiones metodológicas, no resultados empíricos.

### 9.1 Tensión metodológica aún abierta

`PREGUNTA ABIERTA` La V1 separa por diseño señales “internas” y “externas”, mientras pretende estudiar la construcción funcional de la frontera yo/entorno. Esa separación de canales puede aportar al agente información parcial sobre la frontera que se desea observar emerger. La decisión actual no elimina la tensión: la registra como supuesto de arquitectura. Antes de afirmar autodistinción emergente habrá que especificar qué conoce cada módulo sobre el origen del canal y comparar, idealmente, una condición con canales identificados contra otra sin esa identificación.

## 10. Historial

| Versión | Fecha | Estado | Cambios principales |
|---|---|---|---|
| 0.1 | 14/09/2026 | Base conceptual | Hipótesis, arquitectura modular, programa experimental, métricas, falsación y reproducibilidad. Conservada en `.docx`. |
| 0.2 | 14/09/2026 | Especificación epistemológica inicial | Frontera mundo/percepción/modelo, permisos de información, `PatternState`, tick externo, frontera yo/entorno, supuestos y predicción multisensorial. |

## 11. Declaración de trabajo

Este informe no es una defensa de la hipótesis. Su función es permitir que sea entendida, implementada, puesta a prueba, modificada o rechazada. El éxito del proyecto depende de producir afirmaciones con consecuencias observables, registrar las decisiones y aceptar que la hipótesis puede fallar.
