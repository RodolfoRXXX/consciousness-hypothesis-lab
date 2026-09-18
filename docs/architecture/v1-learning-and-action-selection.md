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
s_t ∈ {0,1}²
a_t ∈ {action_0, action_1}
```

`s_t` es el vector completo de dos canales externos binarios definido en [Percepción y estado mínimo](v1-perception-and-state.md). No contiene señales corporales, objeto segmentado, distancia, dirección, tipo ni ID real. `a_t` es una de dos acciones neutrales. El microentorno no requiere navegación.

No existe función de similitud entre estados. Dos símbolos diferentes son claves diferentes:

```text
(0,1) != (1,1)
```

No hay inferencia automática, distancia, vecindad ni transferencia entre ellos. Cualquier conducta común entre estados distintos debe atribuirse a una política heredada, azar, información compartida introducida por la representación o una fuga; no a generalización aprendida. La generalización pertenece a V1.4 y requerirá un mecanismo y controles explícitos.

La memoria usa el vector completo como clave. No hay `pattern_id`: los valores sensoriales no pueden ser aliases de IDs verdaderos, posiciones absolutas, tipos de entidad o metadata.

## 5. Consecuencia corporal sensada

La consecuencia accesible posterior a una acción es un vector de dos canales corporales binarios:

```text
c_t+1 = (c⁻_t+1, c⁺_t+1)
c⁻_t+1, c⁺_t+1 ∈ {0,1}
```

En la documentación del investigador:

- `c⁻` representa intensidad del canal funcionalmente aversivo;
- `c⁺` representa intensidad del canal funcionalmente apetitivo.

En una implementación futura deberían usarse nombres neutrales como `body_signal_0` y `body_signal_1`. El agente no recibe los conceptos aversivo, apetitivo, dolor, placer, bueno, malo, daño o beneficio. La interpretación funcional pertenece al manifiesto experimental.

Los valores binarios son muestras dentro de `[0,1]`; las medias aprendidas sí pueden tomar valores intermedios. Ambos canales provienen de los eventos sensados definidos en el [perfil perceptivo](v1-perception-and-state.md). No son `energy`, `integrity`, sus deltas reales ni una copia de `PrimaryConsequence` en `GroundTruthState`. La condición base no agrega ruido ni latencia variable; la dinámica corporal verdadera que produce los eventos sigue abierta y debe auditarse.

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

La memoria accesible al agente se reduce a una entrada por par `(s,a)`:

```text
M[(s,a)] = {
    n,
    mean_body_signal_0,
    mean_body_signal_1
}
```

Interpretación funcional:

| Campo | Función mínima | Estado de definición |
|---|---|---|
| `n` | Cantidad de observaciones autorizadas del par `(s,a)`. | Requerido. |
| `mean_body_signal_0` | Media histórica exacta de `c⁻`. | Requerido. |
| `mean_body_signal_1` | Media histórica exacta de `c⁺`. | Requerido. |

`M` contiene estadísticas, no episodios individuales. No necesita recuperar “qué ocurrió en el tick 41”. Su clave no puede incorporar tipos verdaderos, coordenadas absolutas ni identidad persistente del motor.

`variability` queda exclusivamente en instrumentación: no es necesaria para predecir por media ni para la política inicial. `next_state_counts` también se elimina de la memoria cognitiva de V1.0–V1.2. `s_t+1` se conserva en `E_t` y `ExperienceTrace`, pero el mecanismo no necesita predecirlo para responder la pregunta corporal. Ambos campos podrían agregarse posteriormente como intervenciones funcionales; no se almacenan “por si acaso”.

## 8. Actualización incremental candidata

Para cada canal corporal se adopta como primera candidata a implementación la media histórica incremental exacta:

```text
mean_(n+1)
= mean_n + (c_(n+1) - mean_n) / (n+1)
```

Ventajas metodológicas:

- cada actualización puede reconstruirse;
- no introduce un learning rate arbitrario;
- conserva dependencia explícita de toda la historia;
- permite comparar estado anterior, observación y estado posterior.

Supone que la regularidad relevante es aproximadamente estacionaria y concede igual peso agregado a toda la historia. Tras invertir contingencias, evidencia antigua puede dominar y producir adaptación lenta. Eso es una predicción y limitación del organismo mínimo, no un defecto que deba corregirse retrospectivamente.

Una fase posterior podrá comparar **media histórica exacta** contra **actualización ponderada por recencia**. Esta última agregaría plasticidad frente a cambio, además de un parámetro y mayor sensibilidad al ruido. No se introduce forgetting factor ni `alpha` para garantizar reversal.

## 9. Predicción y error de predicción

Antes de seleccionar, el predictor consulta una instantánea de `M` y produce para cada acción disponible una predicción one-step:

```text
Prediction(s_t, a) = {
    predicted_body_signal_0,
    predicted_body_signal_1,
    seen_status
}
```

Para cada canal:

```text
delta⁻_t = observed⁻_t+1 - predicted⁻_t+1
delta⁺_t = observed⁺_t+1 - predicted⁺_t+1
```

`prediction_error` es discrepancia entre predicción y observación. No es reward, utilidad, valencia adicional ni señal automática de prioridad. Puede usarse para actualizar `M`, auditar la actualización, calcular métricas y analizar aprendizaje. Cualquier uso para selección, exploración, atención o relevancia sería un mecanismo adicional que debe declararse y controlarse.

Una predicción existe antes de observar `c_t+1`. Una estadística calculada solo después del resultado no demuestra anticipación.

## 10. Estado de exposición, no incertidumbre

V1 usa únicamente:

```text
UNSEEN: n = 0
SEEN:   n > 0
```

`SEEN` significa solo que existe al menos una experiencia para `(s,a)`. No significa conocido, confiable, estable ni de baja variabilidad. Confiabilidad estadística, intervalos y dispersión pertenecen al análisis del investigador. `N_min`, `UNCERTAIN` y `KNOWN` se eliminan del primer organismo; una fase posterior podrá introducir incertidumbre explícita como capacidad adicional.

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

## 12. Selector lexicográfico directo

Cuando todas las acciones disponibles son `SEEN`, el selector candidato aplica:

```text
1. candidates_0 = argmin_a predicted_body_signal_0(s,a)
2. candidates_1 = argmax_{a ∈ candidates_0} predicted_body_signal_1(s,a)
3. action = uniform_random(candidates_1)
```

No existen umbrales `LOW_AVERSIVE/HIGH_AVERSIVE`, `theta_aversive`, suma, resta, pesos ni tasa de intercambio. Esta es una política ordinal/lexicográfica heredada, no una capacidad emergente. Puede ser conductualmente equivalente a alguna utilidad en dominios restringidos; su ventaja metodológica es hacer visible la prioridad normativa.

La afirmación permitida es: “el organismo heredó prioridad ordinal entre canales corporales y aprendió qué pares `(s,a)` predicen sus consecuencias”. No se afirmará que aprendió desde cero qué es bueno o malo.

### Empate exacto

No se introduce tolerancia numérica. Las muestras corporales iniciales son binarias y los primeros protocolos usan contingencias no conflictivas, de modo que la igualdad exacta —por ejemplo medias aversivas exactamente cero— tiene interpretación auditable. La dimensión apetitiva solo se consulta dentro del conjunto con mínima media aversiva exactamente igual.

Si ruido o señales continuas hacen raros los empates, el comportamiento esperado es que la primera dimensión domine. Agregar discretización, redondeo o tolerancia sería una nueva decisión heredada y no puede aparecer silenciosamente en implementación.

### Evitación no absoluta

No existe una regla equivalente a:

```text
if aversive:
    action forbidden forever
```

Una consecuencia aversiva influye sin crear una lista permanente de acciones prohibidas. Sin embargo, una vez que todas las acciones son `SEEN`, la política inicial no contiene exploración persistente. Por eso puede dejar de muestrear una acción desfavorable y fallar en detectar un cambio posterior. Esa limitación se conserva deliberadamente.

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

## 13. Cobertura local mínima

La política inicial es:

```text
si existe al menos una acción UNSEEN en s_t:
    elegir uniformemente al azar entre acciones UNSEEN

si todas las acciones disponibles son SEEN:
    aplicar selector lexicográfico directo
```

Se denomina `minimal local exploration policy` o política de cobertura local, no curiosidad, novelty seeking, interés, deseo de aprender o motivación intrínseca. Garantiza una primera muestra de cada acción disponible bajo el estado exacto; no garantiza confiabilidad ni aprendizaje correcto. Es una predisposición heredada y puede explicar parte de la exposición.

No existe `epsilon` ni exploración persistente. Una vez cubiertas las acciones locales, el agente explota. Esto reduce parámetros, pero predice que puede no descubrir reversals de contingencias conocidas. La exploración persistente será una intervención futura separada.

Todo sorteo usa una fuente de azar causal controlada. El valor de inicialización del RNG es parámetro causal de la corrida y su copia registrada es metadata exclusiva del observador; el agente no recibe ni puede leer la seed.

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
                M(s,a) → c
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

Las cuatro condiciones comparten cuerpo, sensores, acciones, microentorno, oportunidades y transformaciones sensoriales. Para comparaciones causales, P, D y D-ablated reciben durante adquisición una historia emparejada: misma secuencia de estados, acciones ejecutadas y consecuencias sensadas. La forma más limpia es una fase de exposición controlada o *yoked*, no dejar que políticas distintas produzcan historias incomparables. Difieren en las rutas causales disponibles durante prueba:

| Condición | Aprende `M` | Produce predicciones | Predicción entra al selector | Memoria durante prueba | Función |
|---|---:|---:|---:|---:|---|
| **R — Reactive** | No | No | No | Sin `M` cognitiva dependiente de historia | Controlar reacción a señales presentes. |
| **P — Predictive** | Sí | Sí | No | Conservada | Separar predicción aprendida de conducta causada por ella. |
| **D — Decision** | Sí | Sí | Sí | Conservada | Condición mínima completa. |
| **D-ablated** | Sí, antes de prueba | Sí | **No, por intervención específica** | Conservada sin reset | Probar la necesidad causal de `prediction → selection`. |

### R — Reactive

Puede reaccionar a señales actualmente presentes, incluida una señal corporal actual, pero no actualiza ni consulta `M` y no produce predicciones aprendidas. Su política reactiva debe declararse y no recibir fase, patrón verdadero ni contingencia. Si una variante aprende `M` aunque no la use para seleccionar, esa variante pertenece a P, no a R.

### P — Predictive

Aprende y emite predicciones dependientes de historia, pero durante prueba elige `uniform_random(available_actions)`. La política no lee `M`, predicciones ni estado de exposición para seleccionar. El RNG es controlado y registrado externamente.

### D — Decision

Usa cobertura local de acciones `UNSEEN` y, cuando todas son `SEEN`, las mismas predicciones de P mediante el selector lexicográfico. Es la única condición principal que contiene la cadena completa hasta conducta anticipatoria.

### D-ablated

Se deriva de D después de la misma historia. Durante la prueba se cierra exclusivamente la compuerta `prediction → action selection` y se usa `uniform_random(available_actions)`, la misma política de P. No se borra `M`, no se recalculan predicciones con otra historia y no se altera percepción, cuerpo, repertorio o capacidad motora.

Cambiar la salida a una política aleatoria sí cambia el mecanismo proximal de selección; ese es el contenido de la intervención, no una ausencia física de política. Para que sea una ablación interpretable deben verificarse en la misma historia/estado:

```text
predictions_D_before_gate == predictions_D_ablated
```

y deben mantenerse idénticos disponibilidad de acciones, RNG emparejado cuando corresponda y todas las entradas no predictivas. Una alternativa futura aún más localizada sería enmascarar el contenido predictivo manteniendo exactamente el mismo armazón del selector; no aporta ventaja si el fallback ya es uniforme y se demuestra que ninguna otra rama lee predicciones.

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
available actions
action
next_state
body signals
prediction for each action
prediction errors
model before update
model after update
selected action
seen/unseen status
selection mode
candidate actions after each rule
random draw if any
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

### Cobertura diseñada

Priorizar acciones `UNSEEN` garantiza al menos una muestra local y puede hacer posible el aprendizaje que una política puramente aleatoria no observaría en pocas corridas. Es normatividad de exposición, no curiosidad. Una sola muestra cambia el estado a `SEEN`, aunque sea ruidosa o atípica.

### Estado demasiado informativo

Si `s` contiene identidad real, tipo verdadero, coordenada absoluta, objetivo o una segmentación perfectamente alineada con la contingencia, aprender se reduce a lookup privilegiado. Neutralidad nominal no basta.

### Ventana causal regalada

Asignar automáticamente `c_t+1` a `a_t` concede una hipótesis de contigüidad y alineación temporal. V1 la hereda metodológicamente para estudiar la cadena mínima; no demuestra causalidad inferida. Latencias o perturbaciones interpuestas pueden volver falsa esa atribución.

### No estacionariedad y reversal

La media histórica exacta conserva evidencia obsoleta y puede retrasar un reversal. Además, la ausencia de exploración persistente puede impedir que el agente observe la contingencia nueva. Son limitaciones separables: falta de nueva muestra y bajo peso de muestras recientes. Una fase posterior debe intervenir cobertura persistente y recencia por separado.

### Orden y azar

Empates nunca se resuelven por menor índice, orden del array, orden de inserción o ID. Toda selección aleatoria usa un flujo RNG separable. La inicialización causal del RNG es un parámetro experimental; el registro externo de ese valor es metadata. El valor de seed y el estado del RNG no entran al estado cognitivo, aunque los sorteos resultantes afecten la trayectoria.

### Señales corporales y política codificada

La transformación `energy/integrity → body_signal_*`, la topografía estable y los efectos de degradación pueden revelar dirección normativa. El selector minimiza directamente el primer canal y puede producir conducta adaptativa tras una sola muestra por acción. Debe atribuirse por separado la regla heredada y la asociación aprendida.

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
| Entrada sensorial | `RawObservation` con dos canales externos y dos corporales binarios | Se excluyen primitivas y binning adicionales. |
| Estado discreto | `s_t` como vector externo completo | No requiere `PatternState`, ID o entidad. |
| Memoria | `M(s,a)` con `n` y dos medias | Perfil reducido de `MemoryRecord`/`InternalModel`; no episodios, variabilidad ni transiciones. |
| Predicción | Dos medias corporales y estado `SEEN` por acción | Perfil reducido de `Prediction`. |
| Selección | Acción, regla aplicada y uso/no uso de predicción | Perfil reducido de `Decision`; “razón” detallada queda en instrumentación. |
| Observación posterior | `s_t+1`, `c_t+1` | `s_t+1` se conserva pero no se agrega cognitivamente; no requiere `Outcome` semántico. |
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
| señales corporales actuales en clave/selector | No | No | No | No | Sí para control |
| `M(s,a)` | No | Sí | Sí | Sí | Sí, copia externa |
| predicciones one-step | No requeridas | Sí | Sí | Sí | Sí |
| predicciones legibles por selector | No | No | Sí | **No** | Auditable |
| Ground Truth, tick, seed, condición | No | No | No | No | Sí |

Esta tabla define acceso causal, no necesariamente clases o procesos separados.

## 26. Qué aprende, hereda y no usa

### Heredado/diseñado

- dos canales externos binarios y `s` como vector completo;
- dos acciones neutrales y su disponibilidad;
- dos canales corporales binarios, topografía y efectos funcionales;
- estructura de `M`, regla de actualización y ventana t→t+1;
- copia de comando motor;
- distinción `UNSEEN/SEEN` por `n = 0` o `n > 0`;
- cobertura local de acciones `UNSEEN`;
- prioridad lexicográfica directa canal 0→canal 1;
- límites one-step y ausencia de similitud;
- interfaces y puntos de ablación.

### Aprendido

- conteo `n` para cada `(s,a)` visitado;
- media histórica de cada canal corporal sensado por par.

### No usado para elegir en la condición principal

- Ground Truth y metadata;
- delta corporal verdadero;
- `prediction_error` como valor;
- reward, utilidad, Q-value o retorno;
- semejanza con otros estados;
- consecuencias multistep;
- episodios de `ExperienceTrace`;
- `s_t+1` o conteos de transición;
- variabilidad observada;
- señales corporales actuales como parte de `s`;
- labels humanos, identidad o causa real.

## 27. Decisiones candidatas a congelar antes de código

Estas decisiones están suficientemente delimitadas para una revisión de congelamiento posterior, pero continúan **provisionales** mientras no exista ADR o aprobación documental explícita:

- separación Ground Truth / estado sensorial;
- microentorno sin navegación, dos canales externos binarios y dos acciones;
- `s` como vector sensorial externo exacto;
- experiencia `(s,a,s',c)`;
- dos consecuencias corporales binarias y multidimensionales;
- memoria `M(s,a) = {n, mean_body_signal_0, mean_body_signal_1}`;
- media histórica incremental exacta;
- `UNSEEN = n=0` y `SEEN = n>0`, sin `N_min`;
- cobertura exhaustiva local de acciones `UNSEEN`, sin `epsilon`;
- selector lexicográfico directo sin umbrales;
- empate exacto y desempate aleatorio controlado;
- ausencia de reward escalar;
- aprendizaje y predicción one-step;
- predictor causalmente separable del selector;
- ausencia de generalización y planificación;
- `ExperienceTrace` externa;
- controles R/P/D/D-ablated;
- seed registrada solo como metadata;
- capacidad de ablación específica.

La primera ya está congelada por ADR-001. Las restantes no lo están por aparecer en esta lista.

## 28. Decisiones abiertas

- magnitudes y dinámica verdaderas de `energy`/`integrity` bajo cada evento corporal;
- asignación y contrabalanceo de patrones X/Y entre corridas;
- temporización exacta dentro de la ventana causal fija de un paso;
- política, horizonte y métrica de reversal;
- trade-offs aversivo/apetitivo;
- mecanismo futuro de exploración persistente;
- mecanismo futuro de recencia;
- cuándo incorporar estado corporal a `s` para V1.3;
- diseño de generalización para V1.4;
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
- el vector externo es un ID/type one-hot disfrazado o su generación consulta el tipo verdadero;
- P o D-ablated leen predicciones al seleccionar;
- la conducta aparece solo después de la consecuencia corporal;
- las señales sensadas son copias del delta corporal verdadero sin transformación autorizada;
- la media acumulativa aparenta falta de reversal por un horizonte insuficiente;
- los resultados no son reproducibles bajo seeds y condiciones declaradas.

## 30. Auditoría previa a implementación

Antes del primer código debe poder responderse y trazarse:

1. qué propiedades físicas activan los dos bits externos sin consultar tipo real;
2. cómo se deriva cada `body_signal_*` binaria sin exponer Ground Truth;
3. cómo representa numéricamente las medias y preserva empates exactos;
4. cómo se controla el estado corporal inicial al excluirlo de `s`;
5. qué cronograma empareja la historia de P, D y D-ablated;
6. que P y D-ablated usan uniform random sin leer predicciones;
7. qué lee cada ruta y cómo se impiden canales laterales;
8. cómo se genera azar, qué registra la seed y qué nunca ve el agente;
9. cómo se prueba la especificidad de cada ablación;
10. qué métricas separan aprendizaje, predicción y conducta anticipatoria;
11. cómo se evita generalización accidental;
12. qué criterio y horizonte distinguen falta de remuestreo de actualización lenta en reversal;
13. qué perfil de contratos entra realmente a V1.

Si una respuesta permanece abierta, debe convertirse en parámetro o decisión explícita antes de implementación, no resolverse dentro del código.

## 31. Resultado de la auditoría crítica

| Objeción | Resultado de la revisión |
|---|---|
| `s` puede ser un ID disfrazado. | Riesgo real. Se usan componentes físicos compartibles, sin `pattern_id`, con contrabalanceo y auditoría de la transformación. |
| La discretización puede codificar clases. | Se evita binning aprendido o thresholds: los dos sensores son binarios por construcción física. El alfabeto sigue siendo herencia declarada. |
| La política `UNSEEN` garantiza exposición. | Sí, garantiza una muestra por acción/estado y es normatividad heredada. No garantiza confiabilidad ni resultado correcto. |
| Una experiencia otorga demasiado poder. | Riesgo real en entorno determinista. `SEEN` no significa confiable; curvas por número de exposiciones pertenecen al análisis. |
| El selector explica casi toda la adaptación. | Explica la prioridad; la historia determina qué acción predice cada canal. N0/P y reset de `M` separan ambos aportes. |
| R/P/D pueden no ser comparables. | Requieren historias de adquisición emparejadas y mismo microentorno. Sin *yoking*, la comparación no es causalmente limpia. |
| D-ablated cambia de política. | Sí: cerrar la compuerta activa fallback uniforme. Es interpretable solo si predicciones permanecen iguales y el fallback coincide con P. Una intervención de permutación de predicciones puede complementar la prueba. |
| Excluir cuerpo de `s` simplifica artificialmente. | Sí, deliberadamente para V1.0–V1.2 y con estado corporal inicial controlado. V1.3 deberá reintroducir contexto corporal. |
| `(s,a)→c` regala causalidad. | Regala contigüidad y ventana de crédito one-step; se clasifica como herencia metodológica, no inferencia causal emergente. |
| El microentorno elimina embodiment. | Reduce navegación, no cuerpo, sensores, acción o consecuencias. Limita las conclusiones a condicionamiento one-step. |
| Un canal corporal sería suficiente. | Sí para evitación anticipatoria. Se mantienen dos para contrastar además aproximación condicionada y el orden lexicográfico; se exige ablación de canal. |
| Quedan parámetros ocultos eliminables. | Se eliminaron `N_min`, umbrales, tolerancia, `epsilon`, forgetting factor, variabilidad cognitiva y conteos de transición. Persisten dinámica corporal, acoplamiento sensor, temporización y RNG como decisiones explícitas. |

La prueba anticipatoria debe realizarse cuando ambas acciones del estado de prueba sean `SEEN`; de otro modo D ejecutaría cobertura local y no selección por consecuencia predicha.

Para reforzar causalidad de contenido, una intervención complementaria puede intercambiar las predicciones entre `action_0` y `action_1` manteniendo `s`, `M` y selector. Si la elección no sigue el intercambio, la traza declarada no explica causalmente la acción. Esta intervención no reemplaza D-ablated.

## 32. Estado y necesidad de ADR

Este documento no crea ADR-002. La separación epistemológica continúa congelada por ADR-001. La especificación de estados discretos, memoria asociativa, predictor/selector, política normativa y controles todavía es provisional.

Antes de código se recomienda revisar y aceptar mediante ADR el paquete mínimo completo —representación perceptiva, memoria histórica, cobertura local, selector lexicográfico, separación predictor/selector y condiciones R/P/D/D-ablated— porque determina interfaces, normatividad heredada y significado causal de los resultados. Este documento no crea ese ADR. Exponer información prohibida o cambiar la separación interno/externo sí exigiría revisar formalmente ADR-001.
