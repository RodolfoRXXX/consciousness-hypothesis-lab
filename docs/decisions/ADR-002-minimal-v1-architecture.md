# ADR-002 — Arquitectura mínima para V1.0–V1.2

- **Estado:** aceptada
- **Fecha:** 2026-09-18
- **Versión:** 1.0
- **Alcance:** instrumento experimental V1.0–V1.2
- **Depende de:** [ADR-001 — Frontera epistemológica](ADR-001-epistemic-boundary.md)

## Contexto

V1.0–V1.2 debe estudiar separadamente la cadena funcional:

```text
experiencia
→ aprendizaje
→ predicción
→ selección
→ conducta anticipatoria
```

La pregunta que motiva esta decisión es: ¿cuál es la arquitectura artificial mínima que permite intervenir cada transición, mantener explícita la información heredada y evitar reward escalar, semántica precargada y mecanismos cognitivos innecesarios?

Esta arquitectura es un instrumento experimental, no una teoría de consciencia. ADR-001 conserva autoridad sobre la frontera epistemológica:

```text
GroundTruth
    ↓
authorized sensor transformation
    ↓
agent-accessible observation
```

Nunca existe una ruta directa `GroundTruth → cognitive state`.

## Problema

Una arquitectura demasiado rica puede explicar por diseño la conducta que se pretende observar. Navegación, estados semánticos, generalización, reward, planificación o memoria episódica agregarían explicaciones alternativas. Una arquitectura demasiado compacta o acoplada impediría distinguir si el agente aprendió, predijo o utilizó causalmente una predicción.

Se necesita congelar las fronteras causales y representaciones mínimas antes de diseñar el protocolo y el código, sin congelar asignaciones, métricas ni parámetros propios de cada experimento.

## Decisión

### 1. Frontera informacional

El agente solo recibe observaciones externas y corporales producidas por sensores autorizados. No recibe tipo o identidad verdaderos, coordenada o tick absolutos, seed, condición experimental, nombres X/Y, objetivo, causa verdadera, reward, `energy`, `integrity`, sus deltas ni metadata experimental.

El microentorno de V1.0–V1.2 no tiene navegación. Conserva cuerpo, sensores externos, sensores corporales, acciones, consecuencias físicas y una historia individual; excluye locomoción, orientación, mapa, distancia, navegación y planificación espacial. El mundo 2D permanece en el roadmap posterior.

### 2. Estado externo y acciones

El estado predictivo es exactamente:

```text
s_t ∈ {0,1}²

s_t = (
    external_sensor_0,
    external_sensor_1
)
```

Los bits provienen de dos componentes físicos locales neutrales, independientes y recombinables en la interfaz sensorial. No son categorías, tipos, IDs, nombres, one-hot semánticos, distancia, dirección ni objetivo. La generación del sensor no puede consultar `EntityType` para asignar directamente el vector. No existen `pattern_id` ni `entity_id` cognitivos.

La igualdad es exacta: `(0,1) != (1,1)`. No hay similitud, embeddings, interpolación, nearest neighbor, transferencia, pesos compartidos ni generalización.

El repertorio es:

```text
A = {action_0, action_1}
```

Ambas acciones están disponibles en ensayos válidos, carecen de significado cognitivo precargado y deben contrabalancearse. El índice y el orden nunca resuelven una selección.

### 3. Consecuencias corporales

La consecuencia sensada es:

```text
c_t+1 = (body_signal_0, body_signal_1)
body_signal_i ∈ {0,1}
```

Para el investigador, el canal 0 tiene función primaria aversiva y el canal 1 función primaria apetitiva. El agente no recibe esas etiquetas. Los canales no son reward, `energy`, `integrity`, sus deltas ni copias de Ground Truth. La ruta obligatoria es:

```text
world/action interaction
→ physical bodily event
→ authorized body sensor
→ body_signal
→ experience
→ learned prediction
```

La topografía estable evento corporal → canal sensorial es heredada. Un solo canal bastaría para estudiar evitación anticipatoria; se mantienen dos para contrastar evitación y aproximación condicionada con el mismo organismo. La aproximación solo se interpreta limpiamente cuando la dimensión aversiva está empatada. V1.0–V1.2 usa contingencias no conflictivas y asignaciones contrabalanceadas; no estudia tasas de intercambio entre canales.

El estado corporal actual queda fuera de `s_t`. El protocolo deberá controlar su estado inicial. Esto simplifica el condicionamiento externo y no establece una división ontológica mente/cuerpo. V1.3 podrá revisar esta exclusión.

### 4. Experiencia, memoria y aprendizaje

La unidad experimental es:

```text
E_t = (s_t, a_t, s_t+1, c_t+1)
```

`s_t+1` se conserva en la experiencia y la traza, pero V1.0–V1.2 no aprende con él transiciones externas ni lo usa para seleccionar. El emparejamiento `(s_t,a_t) → c_t+1` entrega una ventana de crédito one-step heredada; el agente no descubre desde cero esa relación temporal.

La única memoria cognitiva es:

```text
M[(s,a)] = {
    n,
    mean_body_signal_0,
    mean_body_signal_1
}
```

No contiene episodios, estados siguientes, variabilidad, confianza, novedad, relevancia, valor, Q-values, utilidad, identidad, causalidad ni self-state. Cada media se actualiza mediante:

```text
mean_(n+1) = mean_n + (observed_(n+1) - mean_n) / (n+1)
```

No hay `alpha`, learning rate, forgetting, recency weighting ni gradient descent. Esta media histórica exacta maximiza trazabilidad y deliberadamente dificulta reversal.

Solo existen:

```text
UNSEEN: n = 0
SEEN:   n > 0
```

`SEEN` indica una observación, no confiabilidad. No existen `UNCERTAIN`, `KNOWN`, `N_min` ni umbral de confianza.

### 5. Predicción, cobertura y selección

La arquitectura mantiene una frontera causal intervenible:

```text
MEMORY M
   ↓
PREDICTOR
   ↓
PREDICTION SET
   ↓
SELECTOR
   ↓
ACTION
```

El predictor consulta `M` y produce una predicción por acción; no selecciona. El selector recibe un conjunto de predicciones fijado antes de actuar; no actualiza `M`. El aprendizaje ocurre después de observar la consecuencia y no altera retrospectivamente la predicción registrada.

Mientras existan acciones `UNSEEN`, el selector elige uniformemente entre ellas. Esta cobertura local es una política heredada, no curiosidad, motivación intrínseca ni preferencia. No hay epsilon ni exploración persistente.

Cuando todas las acciones son `SEEN`, la selección es:

```text
C0 = argmin_a predicted_body_signal_0(s,a)
C1 = argmax_{a∈C0} predicted_body_signal_1(s,a)
action = uniform_random(C1)
```

Los empates son exactos, sin tolerancia ni thresholds. Todo azar usa una seed registrada externamente. No se calcula reward, utilidad ponderada ni Q-value.

La prioridad lexicográfica es normatividad heredada. En dominios restringidos puede ser conductualmente equivalente a alguna utilidad escalar; mantener canales separados no elimina normatividad, sino que hace visibles la prioridad, la ausencia de tasa de intercambio y las ablaciones por canal.

El agente hereda canales funcionalmente distintos, prioridad canal 0 → canal 1, cobertura `UNSEEN`, ventana one-step, topografía sensorial estable, acciones y estructura de memoria. Solo aprende qué pares `(s,a)` predicen qué señales corporales. No aprende desde cero qué es “bueno” o “malo”.

### 6. Condiciones causales

| Condición | Memoria/predicción | Política de selección |
|---|---|---|
| **R — Reactive** | No actualiza ni consulta `M`; no usa predicciones aprendidas. | Se fijará en el protocolo sin información extra. |
| **P — Predictive** | Aprende `M` y produce predicciones. | Uniforme entre acciones disponibles, sin leer predicciones. |
| **D — Decision** | Aprende y predice. | Cobertura `UNSEEN`; luego selector lexicográfico. |
| **D-ablated** | Conserva historia, `M` y predicciones de D. | Se cierra solo el acceso prediction → selection; fallback uniforme como P. |

D-ablated conserva estado, cuerpo, sensores, acciones y capacidad motora. Como la intervención cambia el mecanismo efectivo de selección, no constituye por sí sola una prueba causal perfecta.

Por eso se exige además poder permutar el contenido de las predicciones en la entrada del selector, sin modificar `M`, estado, cuerpo, historia, predictor ni acciones. Si la selección sigue la permutación cuando la regla determina una opción, aumenta la evidencia de `prediction content → selection`. La instrumentación registra la intervención y el agente no accede a ella.

Una medición anticipatoria solo es válida si todas las acciones evaluadas son `SEEN`:

```text
n(s, action_0) > 0
n(s, action_1) > 0
```

De lo contrario, la elección puede explicarse por cobertura heredada y no por preferencia condicionada.

### 7. Traza y capacidad de intervención

El agente conserva únicamente `M[(s,a)]`. La `ExperienceTrace` externa puede registrar run, tick, estado, acciones disponibles, acción, estado siguiente, señales corporales, predicciones, errores, modelo antes/después, estado `SEEN`, modo y candidatos de selección, sorteo, intervención, condición, seed y Ground Truth. El agente nunca puede consultarla.

La implementación futura debe permitir intervenir independientemente aprendizaje, predicción, gate prediction → selection, cobertura y cada canal corporal; resetear o congelar `M`; inspeccionar predicciones; y ejecutar el selector con predicciones normales, permutadas o ausentes. Cada ablación debe demostrar que no alteró componentes no objetivo. Se congela esta capacidad causal, no una API.

## Alcance y decisiones no congeladas

ADR-002 congela arquitectura y fronteras causales, no el protocolo. Permanecen abiertos:

- dinámica y necesidad de `energy` e `integrity` en V1.0–V1.2;
- magnitudes físicas, temporización, ensayos, asignaciones X/Y y acción/consecuencia;
- seeds concretas, métricas, tamaño muestral y criterio de reversal;
- ruido, latencia variable, exploración persistente, forgetting y recency;
- generalización, navegación, estado corporal dentro de `s_t` y V1.3+.

V1.0–V1.2 puede requerir solo interacción física → evento corporal interno → sensor corporal autorizado. `energy` e `integrity` siguen en el roadmap provisional para regulación V1.3; este ADR no los elimina ni los exige.

No hay generalización ni planificación. El horizonte es one-step: no hay futuros multistep, retorno acumulado, descuento, ecuaciones de Bellman, búsqueda ni rollout.

## Alternativas consideradas

- **Navegación 2D:** agrega percepción y control espacial innecesarios para la primera pregunta; se posterga.
- **Q-learning o RL convencional:** combina predicción, valoración y decisión de forma menos adecuada para esta primera disección causal; no se considera científicamente inválido.
- **Red neuronal:** introduce representación distribuida, generalización y optimización difíciles de aislar.
- **Un canal corporal:** basta para evitación, pero no permite contrastar evitación y aproximación con el mismo organismo.
- **Thresholds o `N_min`:** agregan parámetros normativos sin necesidad inicial.
- **Epsilon persistente:** ayudaría a reversal, pero introduce exploración continua antes de establecer su necesidad.
- **Forgetting factor:** ayudaría a adaptación, pero oculta primero el límite de la media histórica.
- **Estado corporal en `s_t`:** será importante para regulación, pero confunde el condicionamiento externo inicial.
- **Generalización:** se reserva para V1.4, donde podrá medirse contra el lookup exacto.

## Consecuencias

El organismo podrá registrar asociaciones estado–acción–consecuencia, predecir consecuencias one-step, cambiar selección según historia, mostrar bajo contingencias apropiadas evitación anticipatoria o aproximación condicionada y admitir intervenciones causales.

Probablemente no podrá mostrar reversal robusto, adaptación rápida a no estacionariedad, generalización, planificación, navegación, regulación homeostática rica, autodistinción, body ownership ni aprendizaje causal temporal complejo. Reversal queda limitado por dos causas separadas: falta de remuestreo persistente y falta de recencia en la memoria.

## Riesgos

- Los dos bits pueden actuar como IDs disfrazados si sus fuentes no son físicas, independientes, recombinables y contrabalanceadas.
- Consultar `EntityType` al producir sensores filtraría semántica.
- Cobertura puede producir cambios de acción antes de que todas sean `SEEN`.
- Una observación puede generar una media extrema; la confiabilidad deberá evaluarse externamente.
- El selector contiene normatividad suficiente para producir conducta adaptativa una vez aprendidas las asociaciones.
- P o D-ablated pueden recibir predicciones por una ruta lateral.
- La ventana one-step regala estructura temporal causal.
- Campos, orden, defaults, precisión numérica o metadata pueden filtrar información.
- La traza externa puede contaminar el flujo cognitivo si las interfaces no se aíslan.
- La ausencia de remuestreo y recencia puede confundirse con incapacidad general de reversal.

## Falsabilidad

- Si R reproduce la conducta anticipatoria de D, la explicación histórica queda debilitada.
- Si P selecciona según sus predicciones, existe una fuga causal.
- Si D cambia sin que `M` dependa de historia, no se demostró aprendizaje.
- Si D-ablated conserva el efecto, el gate no es necesario o existe otra ruta.
- Si una permutación relevante no cambia la selección, la predicción registrada no explica causalmente la acción.
- Si resetear `M` no elimina el efecto, esta memoria no es necesaria.
- Si un estado no visto hereda aprendizaje, existe generalización o fuga.
- Si la medición comienza con acciones `UNSEEN`, no prueba preferencia condicionada.
- Si IDs, labels o Ground Truth explican el resultado, la interpretación propuesta es inválida.

## Límite interpretativo

ADR-002 define un organismo artificial mínimo para estudiar asociaciones, predicciones y preferencias anticipatorias funcionales. No demuestra consciencia, experiencia subjetiva, qualia, dolor, placer, deseo, intención consciente, libre albedrío, self ni equivalencia biológica. Los resultados positivos pertenecen inicialmente al nivel funcional.

## Auditoría adversarial de aceptación

| # | Pregunta | Resultado de la revisión |
|---:|---|---|
| 1 | ¿Los bits externos son IDs disfrazados? | Es un riesgo invalidante; se exige que sean componentes físicos recombinables y contrabalanceados. |
| 2 | ¿La generación consulta `EntityType`? | Queda prohibido usarlo para asignar el vector sensorial. |
| 3 | ¿Cobertura explica por sí sola el resultado? | Puede hacerlo antes de cobertura completa; no después bajo la precondición de medición. |
| 4 | ¿El selector contiene toda la conducta? | Contiene normatividad heredada; la historia aporta qué acción predice cada consecuencia. |
| 5 | ¿Una observación causa falsos positivos? | Puede causar una elección; no basta para confiabilidad, que corresponde al análisis. |
| 6 | ¿P está aislado durante selección? | Su política uniforme no puede leer predicciones y esa ausencia deberá auditarse. |
| 7 | ¿D-ablated es específica o es otro agente? | Conserva historia, memoria y predicciones, pero cambia la política efectiva; requiere controles adicionales. |
| 8 | ¿La permutación mejora causalidad? | Sí: manipula contenido a igual memoria, historia y cuerpo, aunque requiere auditoría de rutas laterales. |
| 9 | ¿`all actions SEEN` elimina el confound de cobertura? | Lo elimina durante la ventana medida; no establece por sí solo confiabilidad estadística. |
| 10 | ¿El segundo canal justifica su normatividad adicional? | Permite contrastar aproximación con evitación; debe poder ablacionarse. |
| 11 | ¿La falta de navegación reduce demasiado la pregunta? | Limita validez externa, pero conserva la cadena causal objeto de V1.0–V1.2. |
| 12 | ¿Son necesarios `energy`/`integrity`? | No para esta arquitectura; permanecen provisionales para V1.3. |
| 13 | ¿Hay reward escalar escondido? | No hay escalar, pero sí una política normativa potencialmente equivalente en dominios restringidos; queda explícita. |
| 14 | ¿Hay generalización accidental? | El lookup exacto la excluye; cualquier transferencia es fuga o error. |
| 15 | ¿Puede filtrarse `ExperienceTrace`? | Es un riesgo crítico; el contrato deberá impedir lectura por el agente. |
| 16 | ¿Se congelan parámetros sin necesidad? | No se congelan asignaciones, ensayos, métricas, seeds concretas ni dinámica corporal. |
| 17 | ¿Alguna decisión contradice ADR-001? | No: todo acceso permanece sensor-mediado y la metadata sigue externa. |

La auditoría no encontró una contradicción fundamental. Las objeciones restantes son riesgos controlables o límites declarados, por lo que el ADR queda **aceptado**.

## Perfil contractual siguiente

El siguiente paso documental es definir un perfil contractual V1 mínimo compatible conceptualmente con `ExternalRawObservation`, `BodyRawObservation`, `ExternalState`, `Experience`, `AssociativeMemoryEntry`, `Prediction`, `SelectionTrace`, `ExperienceTrace` y `ExperimentMetadata`.

Ese perfil no reintroducirá automáticamente `SelfState`, `IntegratedState`, `Valuation`, `PatternState` ni un `Outcome` semántico, y preservará la separación entre memoria cognitiva e instrumentación.

## Criterios para reconsiderar la decisión

Revisar ADR-002 si evidencia o una nueva pregunta requiere cambiar la representación sensorial, incorporar estado corporal en la clave, agregar remuestreo o recencia, usar señales continuas que invaliden empate exacto, introducir generalización o planificación, o alterar las condiciones causales. Toda exposición de Ground Truth o cambio de la frontera interno/externo deberá además revisar ADR-001 mediante un nuevo ADR o versión explícita.
