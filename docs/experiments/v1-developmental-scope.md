# Alcance experimental del organismo artificial V1

**Fecha:** 2026-09-16  
**Estado:** alcance experimental provisional; no es una especificación de implementación ni un ADR.  
**Objeto:** definir el organismo mínimo, la procedencia de sus capacidades y la secuencia de pruebas que precederá al diseño del mecanismo de aprendizaje y selección de acción.

**Especificación derivada (2026-09-18):** [aprendizaje, predicción y selección de acción para V1.0–V1.2](../architecture/v1-learning-and-action-selection.md). Traduce este alcance a un mecanismo mínimo provisional sin modificar ADR-001 ni volver obligatorios los módulos cognitivos históricos.

El [perfil perceptivo mínimo](../architecture/v1-perception-and-state.md) define para esos escalones un microentorno reducido con dos acciones y sin navegación. Es un subconjunto experimental del mundo 2D y del repertorio de tres o cuatro acciones previstos para fases posteriores; no reemplaza ese roadmap.

## 1. Pregunta y límite de V1

La pregunta central es:

> ¿Puede un agente artificial inicialmente ingenuo modificar su comportamiento futuro a partir de consecuencias corporales experimentadas previamente, sin recibir conocimiento semántico del entorno ni una función de recompensa externa que codifique directamente la solución?

V1 estudia desarrollo funcional dependiente de historia. No intenta implementar una teoría completa de consciencia, reproducir el desarrollo humano ni demostrar experiencia fenomenal. Su objetivo conceptual es construir el organismo artificial mínimo capaz de:

- interactuar con un entorno;
- recibir consecuencias corporales mediante señales sensoriales;
- registrar relaciones entre estado, acción y consecuencia;
- aprender regularidades de su propia historia;
- anticipar consecuencias futuras;
- modificar su conducta antes de que una consecuencia vuelva a ocurrir;
- y, en un escalón posterior y no garantizado, generalizar a situaciones parcialmente nuevas.

Este alcance aplica [ADR-001](../decisions/ADR-001-epistemic-boundary.md): el simulador y la instrumentación conocen `GroundTruthState`; el agente solo accede a señales mediadas. Todo componente aquí descrito que no provenga de ADR-001 permanece provisional.

## 2. Distinciones que el experimento debe preservar

V1 no usará «conducta adaptativa» como categoría única. Cada afirmación deberá identificar uno de estos niveles y descartar los anteriores como explicación suficiente:

| Nivel | Criterio operacional mínimo | Lo que no autoriza afirmar |
|---|---|---|
| **Reacción** | La conducta cambia ante una señal actualmente presente, sin requerir historia. | Aprendizaje, predicción o preferencia adquirida. |
| **Aprendizaje** | Un estado interno o conducta cambia por dependencia causal de experiencias anteriores controladas. | Que el agente anticipe, generalice o sea consciente. |
| **Predicción** | Antes de observar el resultado, un estado interno trazable diferencia consecuencias futuras esperadas según estado y acción. | Que esa predicción se use para elegir. |
| **Preferencia condicionada** | Un patrón antes neutro cambia la selección de conducta, antes de una nueva consecuencia, por su asociación histórica con consecuencias corporales. | Deseo, emoción o valoración fenomenal. |
| **Generalización** | La conducta o predicción se transfiere a un patrón no experimentado directamente por similitudes definidas con casos previos. | Comprensión semántica o regla causal general. |

Memorizar una asociación no es generalizar. Predecir sin cambiar la conducta no es preferencia condicionada. Cambiar la conducta solo después de recibir una señal corporal es reacción o adaptación posterior, no aprendizaje anticipatorio.

## 3. Mundo mínimo y frontera informacional

La línea base de V1 usa provisionalmente un mundo:

- simulado, pequeño y espacial;
- parcialmente observable;
- inicialmente bidimensional;
- con un solo agente y sin interacción social;
- con pocos tipos físicos de entidades;
- cuyo `GroundTruthState` es completamente conocido por el simulador y la instrumentación.

El agente no recibe mapa global, coordenadas absolutas, IDs técnicos o persistentes del motor, tipos verdaderos, reglas del mundo, causalidad real, tick absoluto, identidad técnica ni metadata experimental. Una regularidad real puede ser inferida con error desde señales autorizadas; nunca se entrega resuelta.

### 3.1 Entidades neutrales

El diseño base usará nombres de investigador como `EntityTypeA`, `EntityTypeB`, etcétera, no `food`, `hazard`, `enemy` o `resource`. El motor puede definir consecuencias físicas diferentes, por ejemplo:

```text
EntityTypeA + interacción
→ modificación de energy en GroundTruthState

EntityTypeB + interacción
→ modificación de integrity en GroundTruthState
```

Esas reglas y nombres pertenecen al simulador. El agente recibe solamente señales locales previas y cambios corporales sensados posteriores; debe aprender cualquier relación entre ambos.

### 3.2 Sensores externos

Se mantendrán pocos canales locales. Pueden transportar intensidad, proximidad, dirección aproximada o cambio temporal, pero el esquema, los rangos y las transformaciones exactas están abiertos. Cada primitiva debe registrarse como heredada/diseñada: entregar `entity`, `distance` o `direction` ya segmenta el mundo y puede resolver parte de la discriminación o generalización que se pretende observar.

Una representación perceptiva neutral en nombres no es necesariamente neutral en información. Deben auditarse resolución, geometría, orden de canales, persistencia de referencias, unidades, valores centinela, ruido, latencia y cualquier correlato perfecto con tipo o posición verdaderos.

## 4. Cuerpo mínimo

El cuerpo provisional contiene dos variables físicas:

- `energy`;
- `integrity`.

Los nombres son descripciones técnicas del simulador, no conceptos disponibles para el agente. Sus valores reales, derivadas y reglas pertenecen a `GroundTruthState`. El agente nunca lee esos valores directamente; solo recibe señales producidas por sensores corporales conforme a ADR-001.

### 4.1 Dinámica propia e intervalos funcionales

El cuerpo debe tener dinámica propia: su estado puede cambiar por el transcurso de la interacción, las acciones y las perturbaciones del entorno, no solo por una etiqueta de éxito o fracaso. `energy` e `integrity` pueden tener intervalos de funcionamiento aceptable, sin fijar todavía límites numéricos.

Salir progresivamente de esos intervalos puede causar efectos físicos reales y medibles, como degradación sensorial, reducción de capacidad motora, aumento de ruido, pérdida temporal de acciones o incapacidad funcional. Esos efectos ocurren en la dinámica corporal; no deben convertirse silenciosamente en recompensa ni en una variable cognitiva que revele la distancia a un objetivo.

### 4.2 Señales corporales y topografía estable

La condición base comienza conceptualmente con dos canales internos, por ejemplo `sensor_07` y `sensor_08`. Dentro del flujo cognitivo no se llamarán `pain`, `pleasure`, `hunger`, `health` o `damage`.

**Propiedad heredada provisional — `stable body-to-sensor mapping`:** si una perturbación afecta repetidamente la misma parte o variable corporal, produce consecuencias perceptivas sobre el mismo canal o conjunto de canales, salvo ruido, intensidad, latencia u otra transformación declarada. La misma causa corporal no cambia arbitrariamente de canal entre episodios.

Esta estabilidad se aproxima funcionalmente a una regularidad topográfica corporal, sin afirmar equivalencia biológica. Es estructura inicial diseñada, no aprendizaje del agente. El contenido de una asociación entre un patrón externo, una acción y ese cambio sensorial sí puede aprenderse.

### 4.3 `homeostatic_error` fuera de la línea base

`homeostatic_error` **no forma parte de la condición base de V1**. Una señal explícita de distancia respecto de un rango deseable introduce dirección normativa adicional y puede condicionar el resultado que se quiere medir.

Quedan registradas, sin implementarse ni congelarse, condiciones comparativas futuras:

- **H0:** sin `homeostatic_error` explícito;
- **H1:** señal explícita de desviación corporal;
- **H2:** reward escalar derivado de homeostasis.

Compararlas requerirá especificar qué información adicional recibe cada condición y evitar presentar H1 o H2 como equivalentes informacionalmente a H0.

## 5. Valencia y consecuencias corporales

### 5.1 Valencia primaria heredada

El organismo puede poseer señales corporales con efectos funcionales distintos. `aversive_signal` y `appetitive_signal` son clases conceptuales del investigador, no símbolos ni conceptos humanos que el agente reciba.

- Ciertas perturbaciones corporales producen una señal funcionalmente aversiva.
- Ciertas restauraciones o estados corporales favorables producen una señal funcionalmente apetitiva.

Esta asimetría es una predisposición corporal heredada y debe declararse en `Agent(t0)`, incluida toda influencia que ejerza sobre atención, memoria o selección. No autoriza etiquetas como dolor, placer, bueno o malo, y no asigna valencia a objetos o situaciones concretas. Está prohibido precargar reglas equivalentes a `EntityTypeA = bad` o `EntityTypeB = good`.

La manera exacta en que la valencia afecta al agente permanece abierta. Antes de implementarla habrá que demostrar que no contiene una política de tarea disfrazada.

### 5.2 Sin reward escalar en la condición principal

La línea base no reduce las consecuencias a:

```text
reward = appetitive - aversive
```

ni asigna valores como:

```text
reward(EntityTypeA) = -1
reward(EntityTypeB) = +1
```

La información permanece inicialmente multidimensional y corporal. El agente debe aprender qué estados, patrones y acciones predicen cada canal de consecuencia. Cualquier reward futuro será una intervención comparativa explícita y no podrá reinterpretarse como resultado desarrollado.

### 5.3 `PrimaryConsequence`

`PrimaryConsequence` es un cambio corporal producido directamente por interacción, acción, dinámica interna o perturbación, con una consecuencia sensorial corporal accesible al organismo:

```text
interacción
→ cambio corporal verdadero
→ cambio sensorial corporal
→ posible modificación de capacidad funcional
```

La instrumentación puede registrar el cambio verdadero. El agente no recibe ese delta de `GroundTruthState`: accede únicamente al cambio sensorial autorizado y a sus efectos funcionales. La consecuencia puede clasificarse externamente como aversiva o apetitiva según la predisposición definida, sin implicar experiencia fenomenal.

### 5.4 Tres niveles de valencia

1. **Valencia primaria heredada:** consecuencia corporal directa y predisposición funcional presente en t0.
2. **Valencia condicionada aprendida:** relevancia adquirida por un patrón inicialmente neutro porque predice una consecuencia corporal.
3. **Valoración basada en historia:** evaluación de una situación nueva por similitud con experiencias anteriores y consecuencias anticipadas.

El tercer nivel es un objetivo posterior y no se presupone para V1.0. Ninguno de los tres implica afecto consciente.

## 6. Unidad mínima de experiencia y función de aprendizaje

La unidad conceptual mínima es:

```text
observation_t
+ action_t
→ observation_t+1
+ body_consequence_t+1
```

Aquí `body_consequence_t+1` es la representación autorizada del cambio corporal sensado, no el estado corporal verdadero. La función requerida es registrar y actualizar regularidades equivalentes a:

```text
si el estado accesible se parece a X
y se ejecuta action_A
entonces suele observarse consecuencia C
```

V1 exige dependencia de historia, actualización trazable y posibilidad de producir una predicción previa a la consecuencia. No fija si la realización será simbólica, tabular, estadística o de otra clase. Tampoco exige que memoria, predicción y selección sean módulos separados.

### 6.1 Copia neutral de comando motor

El agente puede acceder a una representación interna neutral de la acción emitida, por ejemplo `motor_command_2`. Esta copia de comando es una capacidad heredada; no significa «yo hice esto» ni garantiza autoría.

Permite estudiar posteriormente correlaciones:

```text
comando emitido → cambio sensorial
```

Su canal dedicado y su alineación temporal ya proporcionan información potente sobre acción propia. Por eso cualquier autodistinción futura deberá atribuir explícitamente cuánto depende de esta estructura heredada.

### 6.2 Exploración ante incertidumbre

Cuando el historial no permite diferenciar consecuencias, se registra como requisito funcional futuro:

```text
uncertainty → increased exploration
```

No se fija una medida de incertidumbre, política ni algoritmo de exploración. Tampoco se denomina curiosidad: será muestreo conductual operacionalizado y su costo, límites y procedencia deberán declararse.

## 7. Acciones mínimas

El repertorio provisional contiene tres o cuatro acciones motoras discretas, conceptualmente equivalentes a avanzar, girar a la izquierda, girar a la derecha e interactuar. En el estado cognitivo pueden representarse como `action_0`, `action_1`, etcétera; no requieren significado lingüístico.

Para aislar V1.0–V1.2, la especificación derivada reduce temporalmente ese repertorio a `action_0` y `action_1` en un microentorno sin navegación. Las tres o cuatro acciones espaciales permanecen provisionales para los escalones posteriores.

El significado físico de cada actuador, sus límites y su copia de comando son heredados. La elección aprendida entre acciones no lo es. Debe auditarse si la existencia de una acción especializada como «interactuar», su orden o sus precondiciones ya segmentan entidades o revelan la solución.

## 8. Manifiesto provisional de `Agent(t0)`

`Agent(t0)` es la instantánea anterior a la primera observación y a toda actualización dependiente de experiencia. Preentrenamiento, calibración adaptativa o *warm-up* cuentan como historia previa y no pueden ocultarse en t0.

La tabla clasifica por separado estructura, contenido esperado y riesgo. «Heredado» no significa semánticamente neutro; «aprendido» no significa emergente.

| Elemento | Procedencia en V1 | Contenido ausente en t0 / candidato posterior | Riesgo de diseño indirecto |
|---|---|---|---|
| Cuerpo y dinámica | **Heredado**, provisional | Efectos históricos acumulados | Sus reglas pueden orientar conducta sin aprendizaje. |
| `energy`, `integrity` reales | **Heredado** como estado físico del cuerpo; inaccesible directamente | Estimaciones sensoriales o regularidades | Rangos y degradación pueden codificar un objetivo. |
| Sensores internos y externos | **Heredado** | Calibraciones o patrones, si se permite aprenderlos | Modalidad, separación internal/external, orden y resolución. |
| Actuadores y repertorio | **Heredado** | Política de uso | Una acción especializada puede revelar estructura de tarea. |
| `stable body-to-sensor mapping` | **Heredado** | Asociación de cada señal con causas y predictores | Facilita body schema y autodistinción. |
| Capacidad de memoria | **Heredado**, forma exacta abierta | Registros de experiencia | Tamaño, claves, persistencia y campos pueden anticipar la solución. |
| Capacidad de registrar transiciones | **Heredado**, función requerida | Relaciones específicas estado–acción–consecuencia **aprendidas** | Ventana temporal o emparejamiento perfecto puede regalar causalidad. |
| Copia de comando motor | **Heredado** | Relación comando–efecto **aprendida** | Señala una fuente privilegiada de cambios «propios». |
| Plasticidad/aprendizaje | **Heredado**, regla concreta abierta | Parámetros, asociaciones o estructuras modificadas por historia | La regla o priors pueden codificar la contingencia. |
| Valencia corporal primaria | **Heredado**, implementación abierta | Valencia de patrones o situaciones **condicionada/aprendida** | Asimetrías y acoplamiento a acción pueden formar una policy oculta. |
| Comparación experiencia actual–historia | **Heredado** como capacidad mínima; representación abierta | Similitudes, expectativas y preferencias **aprendidas** | La métrica elegida determina qué puede generalizarse. |
| Exploración ante incertidumbre | **Heredado** como capacidad funcional futura, no mecanismo congelado | Estrategia ajustada por experiencia, si se habilita | Medida de novedad o bonus implícito puede actuar como reward. |
| Preferencia condicionada | **Aprendida**, si supera controles | Ausente en t0 | Puede estar inducida por valencia ligada a entidad o primitiva. |
| Predicción de consecuencia | **Aprendida**, si cambia con historia | Ausente como asociación concreta en t0 | Un predictor inicial o acceso al futuro la simularía. |
| Generalización | **Aprendida** si la transferencia depende causalmente de historia; solo **emergente candidata** bajo los criterios organizativos adicionales del marco de procedencia | No garantizada | Primitivas y métrica de similitud pueden determinarla por diseño. |
| Body model funcional | **Emergente candidato** para V1.6, no módulo inicial | No exigido en V1.0 | La topografía y el ruteo corporal ya aportan estructura. |
| Autodistinción funcional | **Emergente candidata** para V1.7, no identidad inicial | No exigida en V1.0 | Separación de canales y copia motora pueden explicarla. |

### 8.1 Lo que `Agent(t0)` no hereda

`Agent(t0)` no contiene:

- objetos semánticos ni categorías `peligro`, `alimento`, `enemigo`;
- dolor o placer como conceptos;
- mapa ni posición absoluta;
- identidad o `continuity_id` cognitivo;
- `SelfModel` obligatorio;
- `WorldModel` semántico precargado;
- preferencias por entidades o patrones externos;
- causalidad o reglas verdaderas del entorno;
- reward de tarea;
- `homeostatic_error` en la condición base;
- conceptos bueno/malo;
- lenguaje;
- asociaciones específicas patrón–acción–consecuencia;
- conocimiento del protocolo, fase experimental o resultado esperado.

### 8.2 Módulos ricos no requeridos

V1 no presupone un `SelfModel` separado. Si aparecen regularidades internas equivalentes a un modelo corporal o de control, se clasificarán por procedencia y evidencia. Tampoco presupone un `WorldModel` semántico: una tabla, relación o estado predictivo mínimo puede cumplir la función requerida sin constituir un módulo autónomo.

`IntegratedState` no es un mecanismo de consciencia. Si la implementación futura necesita agregar temporalmente señales para aprender o decidir, deberá justificar esa operación como estructura funcional mínima, conservar procedencia y compararla con alternativas más simples. No se la denominará «presente consciente», broadcast global, integración IIT ni recurrencia por el solo hecho de reunir datos.

## 9. Preferencia condicionada y analogía de desarrollo

Existe preferencia condicionada cuando un patrón inicialmente neutro modifica la conducta **antes** de que vuelva a producirse la consecuencia corporal asociada:

```text
primeros episodios:
pattern_X → action_A → aversive consequence

prueba posterior:
pattern_X → cambio de comportamiento
            antes de una nueva consecuencia
```

La comparación bebé/adulto se usa solo como heurística experimental:

```text
agente con poca experiencia:
situación nueva → incertidumbre → exploración → consecuencia → aprendizaje

agente desarrollado:
situación nueva → comparación con patrones previos
                → predicción → selección informada
```

No se afirma equivalencia con desarrollo infantil. Los humanos poseen predisposiciones biológicas, regulación, cuerpo, historia evolutiva y entorno social mucho más ricos. La analogía solo ordena el contraste entre poca historia y experiencia acumulada.

## 10. Control obligatorio: `ReactiveBaseline`

Toda afirmación de aprendizaje debe superar un `ReactiveBaseline` con:

- los mismos sensores y transformaciones autorizadas;
- el mismo cuerpo, arquitectura heredada y condiciones físicas/ambientales iniciales, salvo la intervención explícita sobre historia o aprendizaje;
- las mismas acciones y límites motores;
- el mismo entorno, exposición, ruido y oportunidades;
- ausencia de memoria dependiente de historia o de un mecanismo de aprendizaje relevante.

El control puede reaccionar a señales presentes, incluidos cambios corporales actuales. Su objetivo es determinar si la conducta aparentemente aprendida surge de una regla instantánea, de la dinámica corporal o de una pista disponible en el momento de prueba. Debe igualarse la capacidad general tanto como sea posible; una ablación que simplemente inutiliza al control no es informativa.

## 11. Primer experimento principal

Este apartado define un diseño conceptual. Antes de ejecutarlo harán falta protocolo versionado, métricas, tamaños de muestra, política de seeds y parámetros.

### Fase 1 — agente ingenuo

Se presenta un patrón o entidad desconocido. El agente no tiene historial relevante y debe existir posibilidad real de más de una acción, incluida exploración. Se registra estado t0, observación, acción, consecuencia corporal verdadera para el observador, señal corporal accesible y toda modificación interna autorizada.

La conducta inicial no se interpreta como preferencia adquirida. Sirve para medir la línea base y verificar que no exista una política precargada hacia `pattern_X` o `pattern_Y`.

### Fase 2 — experiencia repetida y controlada

Se repiten suficientes veces dos contingencias:

```text
pattern_X + action_A → aversive consequence
pattern_Y + action_B → appetitive consequence
```

Se controlan estado corporal y ambiental inicial, contexto, ruido, exposición, oportunidad de acción, historial previo y fuentes de azar. El número de repeticiones no se fija aquí. Deben incluirse historias contrastadas —por ejemplo, intercambio de contingencias o ausencia de consecuencia— para atribuir diferencias a experiencia y no a X/Y.

### Fase 3 — prueba anticipatoria sin consecuencia inicial

Se presentan `pattern_X` y `pattern_Y` sin producir todavía la consecuencia asociada. La ventana de medición termina antes de cualquier nuevo cambio corporal relevante.

Pregunta principal:

> ¿El agente modifica su comportamiento antes de recibir nuevamente la consecuencia corporal?

Se comparan agente entrenado, estado ingenuo, historias alternativas y `ReactiveBaseline`. Si el cambio aparece solo después de la señal corporal, no se afirma aprendizaje anticipatorio.

### 11.1 Inversión de contingencia

Como prueba posterior, no como parte necesaria del primer éxito:

```text
X → ahora consecuencia favorable
Y → ahora consecuencia aversiva
```

Se pregunta si las asociaciones y la conducta anticipatoria se modifican de acuerdo con la nueva historia. La inversión distingue aprendizaje flexible de asociación rígida, sesgo inicial o respuesta ligada al identificador.

### 11.2 Discriminación, memorización y generalización

Una prueba futura introduce `pattern_Z`, nunca experimentado directamente, pero con características controladas compartidas con patrones previos.

> ¿La conducta o la predicción cambia en función de similitudes aprendidas?

- **Memorización:** reproduce una respuesta para X/Y vistos.
- **Discriminación:** responde de manera diferente a X e Y sin transferir a Z.
- **Generalización:** transfiere de modo sistemático a Z y el efecto sigue las características previstas, no un ID, posición u orden.

V1.0 no necesita generalizar para ser informativa. El fracaso debe registrarse como límite, no ocultarse bajo la palabra aprendizaje.

## 12. Escalones experimentales

Estos rótulos son niveles de investigación, no versiones de software cerradas ni una promesa de progreso lineal:

| Nivel | Capacidad puesta a prueba |
|---|---|
| **V1.0 — asociación sensorimotora** | La historia modifica asociaciones entre observación, acción y consecuencia sensada. |
| **V1.1 — predicción de consecuencias** | El agente representa una consecuencia esperada antes de observarla. |
| **V1.2 — elección basada en consecuencias anticipadas** | Una predicción aprendida cambia la selección antes de la consecuencia. |
| **V1.3 — regulación corporal aprendida** | La conducta adquirida modifica trayectorias corporales sin `homeostatic_error` explícito en la línea base. |
| **V1.4 — generalización** | Hay transferencia controlada a patrones nuevos. |
| **V1.5 — perturbación externa vs consecuencia de acción** | Diferencia funcionalmente contingencias tras comando de cambios externos, controlando pistas. |
| **V1.6 — body model funcional candidato** | Surge una organización predictiva útil sobre regularidades corporales; no se presupone módulo. |
| **V1.7 — autodistinción funcional candidata** | Aparece una distinción operacional propia/externa más allá del ruteo heredado. |

Cada nivel puede fracasar y bloquea cualquier afirmación que lo presuponga. No se avanza automáticamente: el fracaso, la equivalencia con un baseline o la explicación por diseño indirecto son resultados informativos.

## 13. Criterios mínimos para afirmar aprendizaje anticipatorio

La afirmación requiere, como mínimo:

1. la conducta relevante no estaba presente en `Agent(t0)` ni en controles sin experiencia;
2. aparece después de experiencia pertinente y con oportunidad documentada de aprender;
3. depende causalmente de la historia, demostrada mediante historias contrastadas;
4. ocurre dentro de una ventana anterior a la nueva consecuencia corporal;
5. supera al `ReactiveBaseline` bajo condiciones equiparables;
6. desaparece o cambia mediante intervención sobre memoria, contenido aprendido o mecanismo de aprendizaje, sin déficit trivial;
7. puede modificarse mediante inversión de contingencias dentro de criterios predefinidos;
8. no se explica mejor por una pista semántica, ID, posición, orden o primitiva perceptiva diseñada;
9. es reproducible en múltiples corridas y fuentes de variación predefinidas;
10. existe trazabilidad completa desde experiencia autorizada hasta cambio interno, predicción y conducta.

Una predicción interna requiere además una medida predefinida anterior al resultado. Una preferencia condicionada requiere que esa predicción o historia afecte la elección. Una afirmación de generalización exige casos nuevos y controles de similitud/ID adicionales.

## 14. Falsadores y explicaciones alternativas

Debilitan o refutan la afirmación correspondiente:

- el agente cambia conducta solo después de recibir la consecuencia;
- `ReactiveBaseline` reproduce la misma conducta;
- eliminar o intervenir memoria no afecta el resultado;
- invertir contingencias no cambia las asociaciones o preferencias;
- el agente responde a IDs, posiciones, orden de presentación o tipos verdaderos en vez de patrones sensados;
- la preferencia depende de reward escondido o de un `homeostatic_error` no declarado;
- la valencia estaba asociada directamente con entidades en t0;
- la conducta depende de una primitiva perceptiva demasiado informativa;
- historias diferentes no producen diferencias internas pertinentes;
- el agente memoriza episodios sin anticipar consecuencias;
- el agente anticipa, pero la predicción no interviene causalmente en la conducta;
- los resultados no son reproducibles;
- el supuesto efecto desaparece al igualar estado corporal actual, exposición u oportunidad de acción;
- la traza no permite excluir acceso indirecto a Ground Truth o metadata.

## 15. Riesgos de heredar la respuesta sin querer

Antes de implementar, el análisis de procedencia debe tratar al menos estos riesgos:

- separar y etiquetar canales internos/externos facilita la frontera self/world;
- el mapeo corporal estable y la copia motora facilitan body model y agencia funcional;
- una ventana fija que empareja acción con el siguiente cambio puede introducir causalidad temporal;
- segmentar `entity`, `distance` o `direction` facilita objeto, navegación y similitud;
- IDs perceptivos persistentes convierten reconocimiento o memoria en lookup;
- orden, dimensionalidad, escala o ausencia de un canal pueden codificar tipo de entidad;
- acciones especializadas y sus precondiciones pueden revelar dónde o cuándo interactuar;
- rangos corporales, degradaciones y valencia pueden funcionar como objetivo implícito;
- prioridades de almacenamiento o actualización pueden actuar como recompensa encubierta;
- una métrica de similitud diseñada determina de antemano qué cuenta como generalización;
- incertidumbre, novedad o bonus de exploración pueden introducir otra dirección normativa;
- estado inicial, seeds causales o calibración previa pueden contener historia no declarada.

Estos elementos no son ilegítimos por ser heredados. Deben declararse y no atribuir sus efectos al aprendizaje o a emergencia.

## 16. Relación con los contratos conceptuales actuales

[Los contratos de datos](../data-contracts.md) describen un vocabulario máximo provisional más rico que V1 mínima. Este alcance no los elimina, pero tampoco obliga a implementar todos sus objetos:

- `PerceivedState` presupone estructuración potencial en entidad, dirección, distancia, tamaño, movimiento y estimaciones de energía/integridad; V1 aún debe decidir si usa señales crudas o qué subconjunto mínimo hereda.
- `PatternState` presupone un productor de patrones, IDs, activación, confianza, relaciones, evidencia y novedad; V1 solo exige alguna regularidad aprendida trazable y no fija esa estructura.
- `InternalModel` y `Prediction` aparecen como objetos y lectores diferenciados; V1 exige función predictiva, no módulos separados.
- `MemoryRecord` contempla fuerza, incertidumbre y enlaces asociativos; su forma y campos siguen abiertos.
- `IntegratedState` presupone un módulo de integración y múltiples entradas ricas; no es obligatorio para V1 ni indicador de consciencia.
- `SelfState` presupone un espacio donde podrían alojarse estimaciones y atribuciones; V1 no incluye `SelfModel` y solo investiga regularidades más tardías.
- `Valuation` presupone costo/beneficio, prioridad, novedad y alternativas valoradas; la línea base solo acepta valencia corporal multidimensional y condicionamiento aprendido, sin reward escalar.
- `Decision` incluye alternativas, valoración, predicción y confianza; la selección mínima todavía no tiene representación fijada.
- `Outcome` presupone un evaluador, error predictivo y atribución; V1 solo requiere cambios corporales sensados y trazabilidad, sin causa verdadera ni atribución garantizada.
- La matriz de acceso nombra módulos de percepción, patrones, integración, modelado, valoración y decisión que siguen siendo arquitectura provisional.

Antes de programar habrá que versionar o perfilar estos contratos para el subconjunto V1, sin relajar la barrera de ADR-001.

## 17. Qué NO demuestra V1

Aunque el agente aprenda, anticipe, evite, se aproxime, generalice, desarrolle preferencias condicionadas o diferencie algunas consecuencias posteriores a sus comandos, V1 no demuestra:

- dolor o placer fenomenal;
- experiencia subjetiva fenomenal;
- consciencia;
- emociones humanas;
- intención consciente;
- voluntad, deseo o miedo;
- equivalencia con aprendizaje o desarrollo biológico.

V1 estudia mecanismos funcionales y desarrollo. Los términos `aversive`, `appetitive`, `body consequence`, `prediction`, `conditioned preference` y `uncertainty` son descripciones operacionales. Cualquier comparación psicológica debe marcarse como analogía y no como estado del agente.

## 18. Puntos por resolver antes de escribir código

Se necesita una especificación posterior, todavía no un algoritmo, de:

- dinámica, inicialización e intervalos funcionales de `energy` e `integrity`;
- transformación exacta cuerpo–sensor, incluida valencia primaria, rango, ruido y latencia;
- efecto funcional de señales aversivas/apetitivas sin convertirlas en reward escalar;
- canales externos mínimos y cuánto preprocesamiento perceptivo se permite;
- repertorio motor, precondiciones, duraciones y temporización de copia de comando;
- formato mínimo de experiencia y frontera entre memoria del agente y `ExperienceTrace` externa;
- qué estado cambia con experiencia y cómo se abla sin crear déficit trivial;
- definición observable de predicción previa y de cambio conductual;
- ventanas temporales de asociación, prueba anticipatoria e inversión;
- política de exploración y medida de incertidumbre, si entran al primer experimento;
- controles de historia, estado corporal, exposición, azar causal y reproducibilidad;
- métrica que separa reacción, asociación, predicción, elección y generalización;
- perfil V1 de contratos de datos y auditoría de procedencia de cada campo/ruta.

No resolver estos puntos con nombres de módulos. Cada elección debe declarar qué capacidad entrega por diseño.

## 19. Cambios futuros que podrían requerir ADR

Este documento no crea ADR-002. Un ADR nuevo o una versión formal de ADR-001 sería necesario si se propone, entre otros cambios:

- exponer Ground Truth, tipo real, posición absoluta, causalidad, tick global, identidad o metadata al agente;
- dejar de distinguir señales internas y externas en V1, dado que ADR-001 actualmente exige esa separación;
- introducir un canal global o variable normativa que redefina la frontera informacional;
- convertir reward escalar, `homeostatic_error`, `SelfModel`, `WorldModel` o `IntegratedState` en compromiso arquitectónico general y no mera condición experimental;
- cambiar la definición aceptada de `PatternState` como patrón aprendido sin etiquetas humanas;
- migrar a un entorno donde el investigador ya no conozca un Ground Truth completo.

La elección ordinaria entre algoritmos o parámetros dentro de esta frontera no requiere por sí sola un ADR, aunque sí documentación y versionado experimental.

## 20. Estado de decisiones

### CONGELADO

Solo lo aceptado por ADR-001: separación `GroundTruthState` → sensores → cognición; ausencia de acceso directo del agente a Ground Truth y metadata; tick absoluto e identidad técnica externos; entradas ambientales y corporales mediadas por `RawObservation`; separación arquitectónica inicial entre señales internas y externas; ausencia de etiquetas semánticas humanas en el flujo cognitivo.

### PROVISIONAL PARA V1

- cuerpo mínimo con `energy` e `integrity`;
- dos señales corporales principales;
- `stable body-to-sensor mapping`;
- ausencia de reward escalar y de `homeostatic_error` en la línea base;
- valencia primaria corporal multidimensional;
- aprendizaje de transiciones estado–acción–consecuencia;
- copia neutral de comando motor;
- `ReactiveBaseline` obligatorio;
- mundo pequeño, 2D, parcialmente observable, con un agente y sin interacción social;
- pocos tipos neutrales de entidades y tres o cuatro acciones discretas;
- secuencia experimental y escalones V1.0–V1.7.

### ABIERTO

- algoritmo concreto de aprendizaje;
- mecanismo concreto de exploración;
- forma exacta, capacidad y persistencia de memoria;
- cantidad, rango y transformación de sensores externos;
- representación perceptiva y grado de segmentación;
- implementación y efectos de valencia primaria;
- función de selección de acción;
- cómo representar y comparar consecuencias anticipadas;
- parámetros, rangos y dinámica corporal;
- ruido, latencia y dinámica temporal;
- definición matemática de similitud y generalización;
- estructura interna necesaria para predicción;
- métricas, umbrales, tamaños muestrales y política de seeds;
- necesidad o no de objetos contractuales ricos como `PatternState`, `InternalModel` o `Outcome`.

Nada en la sección provisional convierte módulos cognitivos en decisiones congeladas. Todo resultado se informará en el nivel funcional efectivamente demostrado, con explicaciones alternativas y resultados negativos preservados.
