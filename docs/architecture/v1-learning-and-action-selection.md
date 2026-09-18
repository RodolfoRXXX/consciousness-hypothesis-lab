# Aprendizaje, predicción y selección de acción para V1.0–V1.2

**Fecha:** 2026-09-18

**Estado:** especificación funcional provisional previa a código; no es un ADR ni congela el algoritmo final.

**Alcance:** mecanismo mínimo para V1.0–V1.2 del [alcance experimental V1](../experiments/v1-developmental-scope.md).

## 1. Propósito y pregunta funcional

La primera implementación estudiará la cadena causal mínima:

```text
experiencia
→ aprendizaje
→ predicción
→ selección
→ conducta anticipatoria
```

Cada flecha debe poder inspeccionarse e intervenirse por separado. La pregunta funcional principal es:

> ¿Puede una predisposición corporal mínima, combinada con experiencia individual, convertirse en una preferencia anticipatoria hacia patrones que inicialmente eran neutrales?

El objeto es una capacidad funcional de nivel A según la [revisión del estado del arte](../literature/state-of-the-art.md#qué-contaría-como-evidencia). Un resultado positivo no implica consciencia, experiencia fenomenal, deseo, dolor, placer, miedo ni intención consciente.

## 2. Restricciones y exclusiones iniciales

V1.0–V1.2 prioriza interpretabilidad, mínima complejidad, trazabilidad causal, reproducibilidad, ablación y separación entre:

- `GroundTruthState` y estado accesible al agente;
- aprendizaje y decisión;
- predicción y uso de la predicción;
- memoria cognitiva y traza del investigador;
- predisposición heredada y contenido aprendido.

Se excluyen inicialmente redes neuronales, *deep learning*, Q-learning, DQN, transformers, embeddings, backpropagation, reinforcement learning convencional, active inference completo, curiosity-driven learning, algoritmos evolutivos, planificación multistep y generalización por similitud. La exclusión reduce mecanismos y explicaciones alternativas; no afirma que sean inadecuados para fases posteriores.

No se requieren `SelfModel`, `WorldModel`, `IntegratedState` ni módulos semánticos equivalentes. Los nombres funcionales de esta especificación no implican módulos biológicos ni una arquitectura completa de cognición o consciencia.

## 3. Frontera epistemológica

[ADR-001](../decisions/ADR-001-epistemic-boundary.md) permanece íntegramente vigente:

```text
GroundTruthState ──sensores autorizados──> estado accesible
       │                                      │
       └──────── instrumentación ─────────────┴──> observador
```

El agente no recibe valores reales de `energy` o `integrity`, sus deltas verdaderos, tipos o posiciones reales, tick absoluto, seed, escenario, condición experimental, identidad técnica ni etiquetas humanas. El observador puede registrar y relacionar esos datos externamente. La unión de ambas vistas nunca vuelve al agente.

La pertenencia de un valor a `ExperienceTrace` no lo vuelve cognitivamente accesible. La pertenencia a la memoria del agente exige una ruta autorizada desde señales sensoriales o estados derivados de ellas.

## 4. Estados y acciones discretos

Para V1.0–V1.2:

```text
s_t ∈ S
a_t ∈ A
```

`s_t` es un estado perceptivo discreto accesible en el momento t; `a_t` es una acción discreta disponible. `S` y `A` denotan los conjuntos posibles. La representación concreta y sus cardinalidades permanecen abiertas.

No existe función de similitud entre estados. Dos símbolos diferentes son claves diferentes:

```text
pattern_03 != pattern_04
```

No hay inferencia automática, distancia, vecindad ni transferencia entre ellos. Cualquier conducta común entre estados distintos debe atribuirse a una política heredada, azar, información compartida introducida por la representación o una fuga; no a generalización aprendida. La generalización pertenece a V1.4 y requerirá un mecanismo y controles explícitos.

Los identificadores discretos deben ser internos o perceptivos y no aliases de IDs verdaderos, posiciones absolutas, tipos de entidad o metadata.

## 5. Consecuencia corporal sensada

La consecuencia accesible posterior a una acción es un vector de dos canales:

```text
c_t+1 = (c⁻_t+1, c⁺_t+1)
```

En la documentación del investigador:

- `c⁻` representa intensidad del canal funcionalmente aversivo;
- `c⁺` representa intensidad del canal funcionalmente apetitivo.

En una implementación futura deberían usarse nombres neutrales como `body_signal_0` y `body_signal_1`. El agente no recibe los conceptos aversivo, apetitivo, dolor, placer, bueno, malo, daño o beneficio. La interpretación funcional pertenece al manifiesto experimental.

Como rango candidato, no congelado:

```text
c⁻ ∈ [0, 1]
c⁺ ∈ [0, 1]
```

Ambos valores deben provenir de sensores corporales autorizados. No son `energy`, `integrity`, sus deltas reales ni una copia de `PrimaryConsequence` en `GroundTruthState`. Transformación física, calibración, ruido, saturación y latencia siguen abiertos y deben auditarse porque pueden introducir la solución.

Los dos canales no se combinan en reward ni utilidad escalar. Su topografía cuerpo→sensor estable y su efecto funcional diferencial son predisposiciones heredadas, conforme al alcance V1.

## 6. Unidad mínima de experiencia

La experiencia cognitiva mínima queda provisionalmente definida como:

```text
E_t = (s_t, a_t, s_t+1, c_t+1)
```

donde:

- `s_t`: estado perceptivo accesible antes de actuar;
- `a_t`: copia neutral del comando efectivamente ejecutado;
- `s_t+1`: estado perceptivo accesible posterior;
- `c_t+1`: vector de señales corporales sensadas posteriores.

`E_t` no contiene Ground Truth, causa verdadera, reward, tick absoluto, ID técnico, éxito de tarea ni etiqueta de fase. El emparejamiento t→t+1 y la disponibilidad de una copia motora son estructuras temporales heredadas; facilitan aprender contingencias y deben registrarse como diseño, no como causalidad descubierta desde cero.

### Por qué se conserva `s_t+1`

V1.0–V1.2 prioriza consecuencias corporales, pero conserva `s_t+1` para estudiar posteriormente:

```text
acción → cambio sensorial externo
acción → cambio sensorial corporal
```

Esto evita redefinir la experiencia en fases de contingencia sensorimotora, agencia funcional, body model o autodistinción. Conservar el dato no implica que esas capacidades existan ni autoriza atribución propia/externa.

## 7. Memoria asociativa mínima

La memoria accesible al agente puede reducirse a una entrada por par `(s,a)`:

```text
M(s,a) = {
    N,
    expected_next_state,
    expected_body_signal_0,
    expected_body_signal_1,
    variability
}
```

Interpretación funcional:

| Campo | Función mínima | Estado de definición |
|---|---|---|
| `N` | Cantidad de observaciones autorizadas del par `(s,a)`. | Requerido. |
| `expected_next_state` | Frecuencias o estimación discreta de estados posteriores. | Conservado para continuidad; forma exacta abierta. |
| `expected_body_signal_0` | Estimación histórica de `c⁻`. | Crítico para V1.0–V1.2. |
| `expected_body_signal_1` | Estimación histórica de `c⁺`. | Crítico para V1.0–V1.2. |
| `variability` | Dispersión observada por canal o transición. | Requerimiento de auditoría; estimador exacto abierto. |

`M` contiene estadísticas, no episodios individuales. No necesita recuperar “qué ocurrió en el tick 41”. Su clave no puede incorporar tipos verdaderos, coordenadas absolutas ni identidad persistente del motor.

Aunque `expected_next_state` se nombre en singular, para estados categóricos no debe interpretarse como promedio numérico de IDs. Puede ser una distribución de frecuencias u otra representación discreta explícita. Elegirla queda abierto.

## 8. Actualización incremental candidata

Para cada canal corporal, una regla inicial candidata es la media histórica incremental exacta:

```text
mean_(n+1)
= mean_n + (c_(n+1) - mean_n) / (n+1)
```

Ventajas metodológicas:

- cada actualización puede reconstruirse;
- no introduce un learning rate arbitrario;
- conserva dependencia explícita de toda la historia;
- permite comparar estado anterior, observación y estado posterior.

No está congelada. Supone que la regularidad relevante es aproximadamente estacionaria y concede igual peso agregado a toda la historia. Tras invertir contingencias, evidencia antigua puede dominar y producir adaptación lenta.

Dos alternativas quedan abiertas y deben compararse antes de código:

- **A — media histórica exacta:** todo el historial conserva peso;
- **B — actualización con recencia/forgetting factor:** observaciones recientes reciben mayor influencia.

La alternativa B introduciría al menos un parámetro adicional, por ejemplo `alpha`, y un supuesto heredado sobre velocidad de cambio. No debe incorporarse silenciosamente. La prueba de reversal puede justificar B, pero no se decidirá retrospectivamente solo para obtener el resultado esperado.

## 9. Predicción y error de predicción

Antes de seleccionar, el predictor consulta una instantánea de `M` y produce para cada acción disponible una predicción one-step:

```text
Prediction(s_t, a) = {
    predicted_next_state,
    predicted_body_signal_0,
    predicted_body_signal_1,
    evidence_class,
    observed_variability
}
```

Para cada canal:

```text
delta⁻_t = observed⁻_t+1 - predicted⁻_t+1
delta⁺_t = observed⁺_t+1 - predicted⁺_t+1
```

`prediction_error` es discrepancia entre predicción y observación. No es reward, utilidad, valencia adicional ni señal automática de prioridad. Puede usarse para actualizar `M`, auditar la actualización, calcular métricas y analizar aprendizaje. Cualquier uso para selección, exploración, atención o relevancia sería un mecanismo adicional que debe declararse y controlarse.

Una predicción existe antes de observar `c_t+1`. Una estadística calculada solo después del resultado no demuestra anticipación.

## 10. Incertidumbre mínima

V1 usa una clasificación rudimentaria basada en exposición:

```text
UNSEEN:    N = 0
UNCERTAIN: 0 < N < N_min
KNOWN:     N >= N_min
```

`N_min` es un parámetro experimental heredado y explícito; su valor permanece abierto. Esta clasificación representa falta de experiencia, no probabilidad bayesiana ni confianza epistémica completa.

`KNOWN` no significa baja variabilidad ni predicción correcta. Muchas observaciones pueden revelar una contingencia inherentemente variable. Por eso `N` y `variability` se registran por separado. Una fase posterior podrá distinguir incertidumbre por escasez de datos de variabilidad ambiental, pero V1 no introduce un estimador complejo.

## 11. Normatividad sin reward escalar

La condición principal no calcula:

```text
reward = appetitive - aversive
utility = w1 * appetitive - w2 * aversive
Q(s,a)
```

Tampoco usa Bellman equations, retorno acumulado ni descuento temporal. Mantener los canales separados hace visible qué predisposición se incorpora.

Esto no elimina normatividad diseñada. Aparece en dos lugares heredados:

1. los efectos funcionales distintos de los canales corporales;
2. la regla que permite al selector priorizar predicciones de esos canales.

Por tanto, la selección lexicográfica propuesta puede cumplir una función análoga a una preferencia codificada, aunque no sea reward escalar. La afirmación legítima no es “el agente aprendió que lo aversivo debe evitarse”, sino:

> El agente heredó cómo tratar ordinalmente dos canales y aprendió qué pares `(s,a)` predicen sus intensidades.

## 12. Selector lexicográfico provisional

Para contingencias no conflictivas de V1.0–V1.2, el selector candidato sigue este orden conceptual:

1. clasificar evidencia como `UNSEEN`, `UNCERTAIN` o `KNOWN`;
2. entre consecuencias conocidas, distinguir predicción aversiva alta de baja mediante un umbral heredado;
3. priorizar alternativas conocidas con menor clase aversiva;
4. cuando las alternativas sean comparables en la dimensión aversiva, priorizar mayor clase o intensidad apetitiva anticipada;
5. ante información insuficiente, permitir exploración explícita;
6. resolver empates por azar controlado, nunca por orden de colección ni ID de acción.

Esta es una política ordinal/lexicográfica heredada, no una capacidad emergente. Los umbrales, la comparación exacta dentro de cada clase y la prioridad entre `UNKNOWN`, `LOW_AVERSIVE` y `HIGH_AVERSIVE` permanecen abiertas. Una clasificación candidata para estudiar es:

```text
LOW_AVERSIVE
UNKNOWN
HIGH_AVERSIVE
```

con prioridad aproximada:

```text
LOW_AVERSIVE > UNKNOWN > HIGH_AVERSIVE
```

La relación anterior no queda congelada por este documento. Favorecer `UNKNOWN` frente a `HIGH_AVERSIVE` y permitir exploración aun entre acciones conocidas son elecciones normativas que deben parametrizarse y compararse.

### Evitación no absoluta

No existe una regla equivalente a:

```text
if aversive:
    action forbidden forever
```

Una consecuencia aversiva influye sin prohibir permanentemente. Debe conservarse una vía pequeña, explícita y controlada de exploración para hacer posibles inversión de contingencias y adaptación a cambios. La probabilidad y sus condiciones quedan abiertas.

### Conflictos de valencia

El selector inicial no resuelve justificadamente casos como:

```text
action_A: aversive = 0.8, appetitive = 0.9
action_B: aversive = 0.1, appetitive = 0.2
```

No hay evidencia para decidir cuánto componente apetitivo compensa cuánto componente aversivo. Introducir pesos ocultaría esa decisión. Los primeros experimentos deben usar contingencias no conflictivas:

```text
X + action_A → aversive alto, appetitive ≈ 0
Y + action_B → aversive ≈ 0, appetitive alto
```

Los trade-offs multidimensionales quedan fuera de V1.0–V1.2 y deben informarse como problema abierto, no resolverse mediante un orden incidental.

## 13. Exploración mínima

Regla funcional candidata:

```text
si no existe experiencia suficiente:
    explorar entre acciones disponibles
```

Puede conservarse una probabilidad pequeña de exploración con acciones conocidas. `epsilon` es un parámetro candidato, no fijado. Esto no aplica epsilon a Q-values: no existen Q-values.

La exploración es selección aleatoria explícita, no curiosidad, novelty reward, information gain ni intrinsic motivation. Tanto `epsilon` como cualquier prioridad de acciones desconocidas son predisposiciones heredadas. Todo sorteo usa una fuente de azar causal controlada. El valor de inicialización del RNG es un parámetro causal de la corrida y su copia registrada es metadata exclusiva del observador; el agente no recibe ni puede leer la seed. Esta distinción evita tratar un parámetro que cambia la trayectoria como contenido cognitivo.

## 14. Separación causal entre predictor y selector

El flujo obligatorio es:

```text
STATE
  │
  ▼
PREDICT CONSEQUENCE FOR EACH ACTION
  │
  ▼
PREDICTION SET
  │
  ▼
ACTION SELECTOR
  │
  ▼
ACTION
```

El predictor lee `s_t`, acciones disponibles y `M`, pero no selecciona. El selector recibe un conjunto de predicciones congelado para ese paso, pero no actualiza contingencias. La actualización ocurre después de observar `E_t`.

Una implementación futura puede combinar físicamente operaciones, pero debe conservar interfaces, registros e intervenciones equivalentes. Sin esa separación causal no puede distinguirse aprender/predicir de usar una predicción para elegir.

## 15. Flujo funcional completo

```text
              SENSORY STATE
                    │
                    ▼
             EXPERIENCE MODEL
              M(s,a) → c,s'
                    │
                    ▼
           PREDICTIONS BY ACTION
                    │
                    ▼
             ACTION SELECTOR
              │           │
          exploitation  exploration
              │           │
              └─────┬─────┘
                    ▼
                  ACTION
                    │
                    ▼
               BODY + WORLD
                    │
                    ▼
            NEW SENSORY STATE
                    │
                    ▼
             PREDICTION ERROR
                    │
                    ▼
                UPDATE M
```

Es un flujo funcional y auditable, no una afirmación sobre módulos biológicos, consciencia, integración fenomenal o arquitectura cognitiva completa.

## 16. Horizonte estrictamente one-step

V1.0–V1.2 predice solo consecuencias inmediatas de una acción:

```text
(s_t, a_t) → (s_t+1, c_t+1)
```

No implementa cadenas acción→acción futura, planificación, descuento temporal, Bellman equations ni cumulative return. El límite a un paso permite aislar aprendizaje de consecuencias inmediatas. Una conducta que requiera sacrificar una consecuencia inmediata para obtener otra posterior está fuera de alcance.

## 17. Condiciones experimentales R/P/D/D-ablated

Las cuatro condiciones comparten cuerpo, sensores, acciones, entorno, oportunidades, transformaciones sensoriales y, cuando corresponda, historias controladas. Difieren en las rutas causales disponibles:

| Condición | Aprende `M` | Produce predicciones | Predicción entra al selector | Memoria durante prueba | Función |
|---|---:|---:|---:|---:|---|
| **R — Reactive** | No | No | No | Sin `M` cognitiva dependiente de historia | Controlar reacción a señales presentes. |
| **P — Predictive** | Sí | Sí | No | Conservada | Separar predicción aprendida de conducta causada por ella. |
| **D — Decision** | Sí | Sí | Sí | Conservada | Condición mínima completa. |
| **D-ablated** | Sí, antes de prueba | Sí | **No, por intervención específica** | Conservada sin reset | Probar la necesidad causal de `prediction → selection`. |

### R — Reactive

Puede reaccionar a señales actualmente presentes, incluida una señal corporal actual, pero no actualiza ni consulta `M` y no produce predicciones aprendidas. Su política reactiva debe declararse y no recibir fase, patrón verdadero ni contingencia. Si una variante aprende `M` aunque no la use para seleccionar, esa variante pertenece a P, no a R.

### P — Predictive

Aprende y emite predicciones dependientes de historia, pero su política de prueba está aislada de ellas. La política de control exacta permanece abierta; debe predefinirse, usar solo información permitida y, preferentemente, emparejar oportunidades/azar con D sin filtrar predicciones por rutas indirectas.

### D — Decision

Usa las mismas predicciones de P mediante el selector normativo declarado. Es la única condición principal que contiene la cadena completa hasta conducta anticipatoria.

### D-ablated

Se deriva de D después de la misma historia. Durante la prueba se desconecta exclusivamente `prediction → action selection`. No se borra `M`, no se recalculan predicciones con otra historia, no se altera percepción, cuerpo, repertorio o capacidad motora. Debe usar la misma política de fallback predeclarada que P para que la intervención no introduzca una estrategia nueva.

## 18. Predicciones falsables por condición

Estas son predicciones, no resultados asumidos:

```text
R:
no debería mostrar cambio anticipatorio dependiente de historia.

P:
debería poder mostrar predicciones dependientes de historia,
pero no cambio conductual causado por ellas.

D:
debería mostrar predicción dependiente de historia
y modificación anticipatoria de selección.

D-ablated:
debería conservar la predicción aprendida
pero perder específicamente su efecto sobre la selección.
```

Interpretaciones adversas:

- si R reproduce D, la explicación por aprendizaje anticipatorio queda debilitada;
- si P cambia conducta como D, hay fuga predictor→selector, política de control inadecuada u otra variable histórica;
- si D no predice antes del resultado, no se demostró predicción;
- si D predice pero no cambia selección, no se demostró preferencia anticipatoria;
- si D-ablated pierde también predicción, memoria o capacidad motora, la ablación no es específica;
- si D-ablated conserva la conducta, la conexión no es causalmente necesaria, existe otra ruta o la ablación fue insuficiente;
- si distintas historias no cambian `M` o sus predicciones, no se demostró aprendizaje dependiente de historia.

La intervención causal principal es comparar D y D-ablated después de historia y estado interno equivalentes, verificando que la predicción persista y que solo desaparezca su lectura por el selector.

## 19. Memoria cognitiva y `ExperienceTrace`

### Memoria accesible al agente

Inicialmente puede consistir solo en `M(s,a)` y las estadísticas necesarias para actualizarlo. No contiene episodios completos, tick absoluto, seed, condición, Ground Truth ni razón experimental.

### `ExperienceTrace` del observador

Registra externamente, por episodio:

```text
run
tick
state
action
next_state
body signals
predictions
prediction errors
model before update
model after update
selected action
selection reason
experimental condition
seed
Ground Truth autorizado al observador
```

El agente nunca consulta `ExperienceTrace`, ni directamente ni mediante una vista que reúna campos no disponibles cognitivamente. `selection reason` es una explicación mecánica de qué regla/empate produjo la acción, no intención o justificación consciente.

## 20. Ablaciones requeridas por diseño

La arquitectura futura debe admitir conceptualmente:

```text
learning_enabled = true/false
prediction_enabled = true/false
prediction_used_for_selection = true/false
exploration_enabled = true/false
```

Estos nombres documentan puntos de intervención; no son todavía flags ni una API. También debe poder:

- congelar `M` sin borrarlo;
- resetear solo memoria y verificar el estado vacío;
- conservar memoria/predicciones y desconectar el selector;
- inspeccionar predicciones sin ejecutar acciones;
- reproducir la misma historia sensorial con políticas distintas cuando el protocolo lo permita;
- conservar interfaces y capacidad general al ablar;
- registrar qué ruta fue intervenida y comprobar ausencia de rutas laterales.

## 21. Ausencia deliberada de generalización

V1.0–V1.2 no usa embeddings, distancias entre estados, nearest neighbor, kernels, features compartidos con una función de similitud ni redes que transfieran entre patrones. `M(s,a)` es un lookup por clave discreta autorizada.

Debe auditarse generalización accidental por:

- colisiones o normalización de IDs perceptivos;
- componentes compartidos de `s` que el selector lea fuera de `M`;
- defaults comunes dependientes de categoría;
- inicialización o prior diferente por tipo verdadero;
- orden estable de estados o acciones;
- transformaciones sensoriales que ya agrupen entidades.

V1.4 podrá añadir representación compartida o similitud como intervención y medir la capacidad nueva frente a este baseline.

## 22. Riesgos conceptuales y diseño indirecto

### Reward escondido

La regla lexicográfica es normatividad heredada y puede ser conductualmente equivalente a algunas funciones de recompensa en escenarios limitados. La diferencia demostrable es representacional y experimental: conserva dimensiones separadas y evita fijar una tasa de intercambio. No debe presentarse como ausencia total de preferencia diseñada ni como superioridad ontológica frente a reward escalar.

### Umbrales diseñados

`HIGH_AVERSIVE`, `LOW_AVERSIVE` y cualquier comparación apetitiva requieren umbrales o reglas heredadas. Pueden determinar la política aun con poco aprendizaje. Deben registrarse, variarse y no optimizarse sobre el resultado final sin declarar esa historia.

### Exploración diseñada

`epsilon`, prioridad de `UNKNOWN` y distribución de muestreo son predisposiciones. Pueden explicar exposición y conducta; no son curiosidad adquirida.

### Estado demasiado informativo

Si `s` contiene identidad real, tipo verdadero, coordenada absoluta, objetivo o una segmentación perfectamente alineada con la contingencia, aprender se reduce a lookup privilegiado. Neutralidad nominal no basta.

### Ventana causal regalada

Asignar automáticamente `c_t+1` a `a_t` concede una hipótesis de contigüidad y alineación temporal. V1 la hereda metodológicamente para estudiar la cadena mínima; no demuestra causalidad inferida. Latencias o perturbaciones interpuestas pueden volver falsa esa atribución.

### No estacionariedad y reversal

La media histórica exacta conserva evidencia obsoleta y puede retrasar o impedir un reversal dentro del horizonte experimental. Un forgetting factor mejora adaptación pero añade recencia diseñada y sensibilidad a ruido. Deben predefinirse criterio de reversal, horizonte, balance de exposiciones y qué resultado distingue rigidez de insuficiente oportunidad.

### Orden y azar

Empates nunca se resuelven por menor índice, orden del array, orden de inserción o ID. Toda selección aleatoria usa un flujo RNG separable. La inicialización causal del RNG es un parámetro experimental; el registro externo de ese valor es metadata. El valor de seed y el estado del RNG no entran al estado cognitivo, aunque los sorteos resultantes afecten la trayectoria.

### Señales corporales y política codificada

La transformación `energy/integrity → body_signal_*`, la topografía estable, los rangos funcionales y los efectos de degradación pueden revelar dirección normativa o entidad. El selector aversivo→apetitivo puede producir adaptación con muy pocas muestras. Deben compararse sensibilidad y futuras condiciones normativas, no atribuir todo el efecto a aprendizaje.

### Identidad y semántica

`s`, `M`, predicciones y copias motoras no contienen “yo”, pertenencia corporal, intención, nombres semánticos ni IDs persistentes del motor. La clave persistente `(s,a)` permite continuidad estadística de un patrón, no identidad personal.

## 23. Condiciones normativas futuras

Sin implementarlas en V1 inicial, se registran comparaciones posibles:

| Condición | Normatividad disponible | Pregunta |
|---|---|---|
| **N0 — prediction only** | Aprende consecuencias; ninguna predisposición usa esos canales como preferencia. | ¿La predicción sola cambia conducta? No debería asumirse. |
| **N1 — consecuencias físicas sin valencia explícita adicional** | Solo degradación o restauración funcional del cuerpo. | ¿La dinámica física basta para algún patrón anticipatorio? |
| **N2 — valencia primaria + condicionamiento** | Canales funcionalmente distintos y selector heredado. | Condición propuesta para D. |
| **N3 — reward/homeostatic controller explícito** | Objetivo escalar o error homeostático diseñado. | Baseline de normatividad más fuerte. |

Pregunta comparativa:

> ¿Cuál es la mínima normatividad heredada necesaria para pasar de predecir consecuencias a adquirir preferencias anticipatorias?

No se asume qué condición será suficiente. N1 requiere cuidado: una degradación que elimina acciones puede cambiar conducta físicamente sin aprendizaje y debe separarse de selección anticipatoria.

## 24. Perfil contractual mínimo V1

[Los contratos conceptuales](../data-contracts.md) describen un vocabulario máximo más rico. Para V1.0–V1.2 se propone este perfil, sin modificar todavía el documento base:

| Necesidad V1 | Contrato mínimo | Relación con contratos actuales |
|---|---|---|
| Estado verdadero e instrumentación | Vista externa de `GroundTruthState` | Se mantiene, nunca accesible al agente. |
| Entrada sensorial | `RawObservation` y, solo si hace falta discretizar, un `PerceivedState` mínimo | Se excluyen primitivas no necesarias. |
| Estado discreto | `s_t` opaco derivado de señales autorizadas | No requiere un `PatternState` rico ni afirma patrón emergente. |
| Memoria | `M(s,a)` con conteos/estimaciones | Perfil reducido de `MemoryRecord`/`InternalModel`; no episodios. |
| Predicción | Vector one-step por acción con evidencia | Perfil reducido de `Prediction`. |
| Selección | Acción, regla aplicada y uso/no uso de predicción | Perfil reducido de `Decision`; “razón” detallada queda en instrumentación. |
| Observación posterior | `s_t+1`, `c_t+1` | No requiere causa verdadera ni `Outcome` semántico. |
| Auditoría | `ExperienceTrace` y `ExperimentMetadata` externos | Se mantienen y no son legibles por el agente. |

Contratos excesivos o no requeridos para este perfil:

- `PatternState`: activación, confianza, relaciones, evidencia y novedad exceden el lookup discreto inicial;
- `InternalModel`: relaciones generales e historial de actualización pueden reducirse a `M`;
- `IntegratedState`: no se necesita agregador de presente;
- `SelfState`: no se estudia self en V1.0–V1.2;
- `Valuation`: costo/beneficio, relevancia y novedad pueden ocultar reward; el selector lee los dos canales sin objeto de valoración separado;
- `Outcome`: error predictivo y cambio sensado pueden calcularse sin evaluador ni atribución causal;
- `Decision`: alternativas valoradas y confianza son más ricas que la selección mínima;
- `PerceivedState`: entidad, distancia, movimiento o energía/integridad percibidas solo entran si el protocolo las justifica.

No son incompatibles como vocabulario futuro, pero serían compromisos innecesarios para la primera arquitectura. La opción recomendada posteriormente es **C: definir perfiles versionados dentro de `data-contracts.md`**, preservando contratos generales y declarando el subconjunto de cada experimento. A (versionar todo el documento) multiplica versiones; B (crear `data-contracts-v1.md`) arriesga divergencia. Esta recomendación no reestructura contratos ni congela la decisión.

## 25. Información por condición y momento

| Información | R | P | D | D-ablated | Observador |
|---|---:|---:|---:|---:|---:|
| `s_t`, acciones disponibles | Sí | Sí | Sí | Sí | Sí |
| `c_t` sensado actual | Sí | Sí | Sí | Sí | Sí |
| `M(s,a)` | No utilizable históricamente | Sí | Sí | Sí | Sí, copia externa |
| predicciones one-step | No requeridas | Sí | Sí | Sí | Sí |
| predicciones legibles por selector | No | No | Sí | **No** | Auditable |
| Ground Truth, tick, seed, condición | No | No | No | No | Sí |

Esta tabla define acceso causal, no necesariamente clases o procesos separados.

## 26. Qué aprende, hereda y no usa

### Heredado/diseñado

- estados y acciones discretos y su disponibilidad;
- canales corporales, topografía y efectos funcionales;
- estructura de `M`, regla de actualización y ventana t→t+1;
- copia de comando motor;
- clasificación por `N`, `N_min` y umbrales elegidos;
- regla lexicográfica y política de exploración;
- límites one-step y ausencia de similitud;
- interfaces y puntos de ablación.

### Aprendido

- conteos y frecuencias para cada `(s,a)` visitado;
- consecuencias corporales sensadas esperadas por par;
- transición discreta posterior, si se activa esa parte;
- variabilidad observada según el estimador elegido.

### No usado para elegir en la condición principal

- Ground Truth y metadata;
- delta corporal verdadero;
- `prediction_error` como valor;
- reward, utilidad, Q-value o retorno;
- semejanza con otros estados;
- consecuencias multistep;
- episodios de `ExperienceTrace`;
- `expected_next_state` salvo que un protocolo posterior autorice explícitamente su uso;
- labels humanos, identidad o causa real.

## 27. Decisiones candidatas a congelar antes de código

Estas decisiones están suficientemente delimitadas para una revisión de congelamiento posterior, pero continúan **provisionales** mientras no exista ADR o aprobación documental explícita:

- separación Ground Truth / estado sensorial;
- estados discretos en V1.0–V1.2;
- experiencia `(s,a,s',c)`;
- consecuencias corporales multidimensionales;
- ausencia de reward escalar;
- aprendizaje y predicción one-step;
- predictor causalmente separable del selector;
- ausencia de generalización y planificación;
- `ExperienceTrace` externa;
- controles R/P/D/D-ablated;
- desempate aleatorio controlado;
- seed registrada solo como metadata;
- capacidad de ablación específica.

La primera ya está congelada por ADR-001. Las restantes no lo están por aparecer en esta lista.

## 28. Decisiones abiertas

- media histórica exacta o forgetting factor;
- regla completa de actualización y estimador de variabilidad;
- `N_min` y definición exacta de incertidumbre;
- umbral aversivo y clasificación LOW/HIGH;
- comparación apetitiva y prioridad exacta UNKNOWN/LOW/HIGH;
- `epsilon`, distribución y condiciones de exploración;
- transformación cuerpo→sensor;
- representación concreta y cardinalidad de `S`;
- número y disponibilidad exactos de acciones;
- temporización, ventana causal, ruido y latencia;
- política, horizonte y métrica de reversal;
- trade-offs aversivo/apetitivo;
- representación de `expected_next_state`;
- política de fallback común a P y D-ablated;
- si `variability` integra el primer perfil o solo la traza;
- perfil contractual definitivo y forma de versionarlo.

## 29. Falsadores de la interpretación

No se afirmará la cadena causal propuesta si ocurre cualquiera de estos resultados sin explicación controlada:

- R reproduce el cambio anticipatorio de D;
- P modifica conducta usando información predictiva;
- D cambia conducta sin que `M` o predicciones dependan de historia;
- D-ablated conserva el efecto de D con la conexión verificada como ausente;
- resetear `M` no altera predicciones o conducta anticipatoria;
- congelar aprendizaje no produce la trayectoria predefinida esperada;
- el supuesto aprendizaje depende de ID real, posición, orden o label;
- `prediction_error`, Ground Truth o metadata llegan al selector;
- el desempate es determinista por índice;
- estados no vistos heredan estimaciones de estados distintos;
- la conducta aparece solo después de la consecuencia corporal;
- las señales sensadas son copias del delta corporal verdadero sin transformación autorizada;
- la media acumulativa aparenta falta de reversal por un horizonte insuficiente;
- los resultados no son reproducibles bajo seeds y condiciones declaradas.

## 30. Auditoría previa a implementación

Antes del primer código debe poder responderse y trazarse:

1. qué campos exactos componen `s` y qué información diseñan;
2. cómo se deriva cada `body_signal_*` sin exponer Ground Truth;
3. cuál es la regla de actualización y cómo maneja no estacionariedad;
4. qué significa `variability` y si afecta o no decisiones;
5. valores o rangos preregistrados de `N_min`, umbrales y exploración;
6. qué política aislada comparten P y D-ablated;
7. qué lee cada ruta y cómo se impiden canales laterales;
8. cómo se genera azar, qué registra la seed y qué nunca ve el agente;
9. cómo se prueba la especificidad de cada ablación;
10. qué métricas separan aprendizaje, predicción y conducta anticipatoria;
11. cómo se evita generalización accidental;
12. qué criterio y horizonte definen reversal exitoso o fallido;
13. qué perfil de contratos entra realmente a V1.

Si una respuesta permanece abierta, debe convertirse en parámetro o decisión explícita antes de implementación, no resolverse dentro del código.

## 31. Estado y necesidad de ADR

Este documento no crea ADR-002. La separación epistemológica continúa congelada por ADR-001. La especificación de estados discretos, memoria asociativa, predictor/selector, política normativa y controles todavía es provisional.

Antes de código convendría un ADR si se desea convertir en compromiso estable el paquete mínimo completo —especialmente la separación predictor/selector, ausencia de reward escalar y condiciones R/P/D/D-ablated— porque determina interfaces, comparabilidad y significado causal de los resultados. La fórmula exacta de actualización, umbrales o `epsilon` podrían documentarse como parámetros experimentales si no alteran la frontera arquitectónica; exponer información prohibida o cambiar la separación interno/externo sí exigiría revisar formalmente ADR-001.
