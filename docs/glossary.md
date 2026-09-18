# Glosario operativo

**Versión:** 0.1 — 2026-09-14  
Estas definiciones describen el estado actual del proyecto. No son definiciones universales ni resultados experimentales.

**Actualización metodológica (2026-09-15):** las entradas nuevas remiten al [marco de procedencia del desarrollo](development/inheritance-learning-emergence.md). La arquitectura cognitiva es **PROVISIONAL — PENDIENTE DE REVISIÓN TEÓRICA Y EXPERIMENTAL**.

## Ablación

Intervención controlada que elimina, desactiva o altera un módulo para medir su contribución causal. Debe preservar tanto como sea posible las demás condiciones y declarar déficits esperados y explicaciones alternativas.

## Aprendido

Contenido o estructura interna modificada por dependencia causal de la historia individual de señales y consecuencias autorizadas. Cambiar con el tiempo o con azar no basta: se requieren historias contrastadas, estado inicial controlado y traza del mecanismo modificado.

## Apetitivo / `appetitive`

Clasificación funcional del investigador para una señal corporal primaria asociada por diseño con una restauración o estado corporal favorable, o para un patrón que posteriormente la predice. No significa placer, gusto, deseo ni «bueno» para el agente. La condición base V1 conserva esta señal como dimensión corporal y no la reduce a reward escalar.

## Aversivo / `aversive`

Clasificación funcional del investigador para una señal corporal primaria producida por ciertas perturbaciones, o para un patrón que posteriormente la predice. No significa dolor, miedo, sufrimiento ni «malo» para el agente.

## Agencia

Capacidad funcional de seleccionar acciones y aprender relaciones entre acciones registradas y consecuencias percibidas. La atribución entre cambio propio y perturbación externa es una pregunta experimental; agencia no implica libre albedrío metafísico.

## Autorreferencia

Uso de regularidades internas relacionadas con estados, acciones e historia del propio sistema dentro de su procesamiento. No requiere lenguaje, un identificador técnico ni una entidad observadora separada.

## Consciencia

`HIPÓTESIS` Posible propiedad emergente de una organización dinámica que integra percepción, patrones, memoria, modelos internos, predicción, presente, autorrepresentación, valoración y decisión. Es una formulación funcional provisional: implementar sus módulos no demuestra consciencia y los experimentos pueden obligar a modificarla o rechazarla.

La frase anterior conserva la hipótesis inicial. La misión refinada estudia primero desarrollo y capacidades funcionales; «emergente» en esa hipótesis no es un resultado ni satisface todavía el criterio operacional de emergencia. Las organizaciones candidatas y la experiencia fenomenal son niveles de afirmación distintos.

## Desarrollo individual

Transformación de estados, modelos y conducta durante la historia de un mismo agente, desde `Agent(t0)`. No equivale a evolución heredable entre generaciones ni garantiza aprendizaje o emergencia.

## Consecuencia corporal / `body consequence`

Cambio corporal que produce señales internas autorizadas y puede modificar capacidades funcionales. El cambio verdadero pertenece a `GroundTruthState`; el agente accede solo a su consecuencia sensorial. Una `PrimaryConsequence` es una consecuencia corporal directa, no una etiqueta de éxito, reward ni afirmación fenomenal.

## Exploración

Variación o muestreo de acciones ante información insuficiente bajo una regla operacional declarada. El requisito futuro `uncertainty → increased exploration` no presupone curiosidad humana ni fija todavía un algoritmo.

## Diseñado indirectamente / inducido

Bandera de auditoría para una capacidad aparentemente adquirida que puede explicarse total o parcialmente por pistas implícitas en canales, primitivas, ruteo, recompensa, nombres, inicialización o entrenamiento. Un sesgo heredado declarado puede ser legítimo; atribuirle a la experiencia lo que aportó el diseño no lo es.

## Emergente (propiedad candidata)

Propiedad organizativa ausente como contenido explícito en t0 y no codificada como respuesta directa en reglas, etiquetas o recompensas, que surge reproduciblemente bajo condiciones definidas de la interacción de mecanismos simples, se mide a un nivel superior y responde de modo explicable a intervenciones causales. No significa solo «no programada explícitamente» ni implica consciencia.

## Experiencia subjetiva

En el alcance funcional del proyecto, variación de la representación y respuesta de un sistema debida a sus canales perceptivos, historia, arquitectura y estado interno particulares. La divergencia de representaciones ante una misma realidad es una predicción estudiable, no prueba de experiencia fenomenal ni de consciencia.

## Falsabilidad

Propiedad de una hipótesis cuyas consecuencias permiten especificar observaciones que la debilitarían o refutarían. Exige registrar criterios antes del resultado y no reformular retrospectivamente la hipótesis para protegerla.

## Mapeo corporal estable / `stable body-to-sensor mapping`

Predisposición heredada por la cual perturbaciones repetidas sobre la misma parte o variable corporal afectan el mismo canal o conjunto de canales, salvo transformaciones declaradas de ruido, intensidad o latencia. Es estructura inicial, no aprendizaje ni body model adquirido.

## Ground truth

Estado operacional verdadero definido y conocido por el motor del entorno simulado: propiedades, posiciones, tipos y causalidad reales dentro de la simulación. Es una referencia experimental del observador y nunca una entrada directa del agente; no constituye una tesis ontológica sobre la realidad.

## Heredado

Estructura, capacidad, predisposición o contenido presente en `Agent(t0)` antes de experiencia individual. **Estructura heredada** (poder aprender asociaciones) se distingue de **conocimiento heredado** (una asociación específica ya precargada). Una condición inicial del experimento puede afectar causalmente el desarrollo y debe declararse por separado.

## Metadata experimental

Información exclusiva para reproducir y auditar una ejecución, como `run_id`, ID técnico del agente, tick absoluto, seed, escenario, versión, commit, configuración, módulos, Ground Truth y etiquetas humanas. No puede influir en el agente.

El registro externo de una condición es metadata; el sensor, cuerpo o parámetro configurado en esa condición puede tener efecto causal por vías autorizadas. **Metadata experimental ≠ conocimiento del agente.**

## Nacimiento experimental / `Agent(t0)`

Instantánea anterior a primera observación y a aprendizaje por experiencia individual: arquitectura, parámetros, estado interno, conocimiento inicial, sesgos y cuerpo. Preentrenamiento o precalibración cuentan como historia previa y deben declararse.

## Modelo interno

Representación modificable construida por el sistema sobre regularidades, relaciones y consecuencias esperadas usando únicamente información accesible. No necesita ser simbólica ni lingüística y no es una copia garantizada del mundo real.

## Patrón

Estructura o activación interna aprendida a partir de combinaciones recurrentes de percepción, memoria y consecuencias. Su identificador no lleva semántica humana. Una interpretación como “amenaza” pertenece al investigador, no al patrón.

## Predicción

Estado interno trazable, producido antes del resultado, que diferencia consecuencias futuras esperadas a partir de información accesible e historia. Anticipar no implica usar la predicción para elegir ni implica consciencia.

## Error de predicción / `prediction_error`

Diferencia entre una consecuencia sensorial predicha antes de actuar y la observada después. En V1.0–V1.2 se conserva por canal corporal para actualización y auditoría; no es reward ni señal automática de valor, selección o exploración.

## Preferencia condicionada

Cambio de conducta ante un patrón inicialmente neutro, ocurrido antes de una nueva consecuencia corporal y dependiente de la asociación histórica entre ese patrón, acciones y consecuencias. Se distingue de reaccionar a una señal corporal presente y no equivale a deseo.

## `ReactiveBaseline`

Control con el mismo cuerpo, sensores, acciones y entorno que el agente estudiado, pero sin memoria dependiente de historia o sin el mecanismo de aprendizaje relevante. Una afirmación de aprendizaje debe superar este control bajo condiciones equiparables.

## Selector lexicográfico

Regla normativa heredada que ordena alternativas por dimensiones sucesivas sin reducirlas a una suma escalar. En V1.0–V1.2 prioriza provisionalmente clases de consecuencia aversiva y solo después la dimensión apetitiva. No es una preferencia aprendida, puede explicar conducta por diseño y sus umbrales permanecen abiertos.

## `UNSEEN` / `UNCERTAIN` / `KNOWN`

Clasificación mínima de evidencia según cantidad de observaciones de un par estado–acción. Representa falta de experiencia de forma rudimentaria; `KNOWN` no garantiza baja variabilidad ni una predicción correcta.

## Valencia primaria

Predisposición corporal heredada por la cual distintas señales tienen efectos funcionales aversivos o apetitivos. No asigna semántica a entidades ni equivale a reward escalar, dolor o placer.

## Valencia condicionada

Relevancia aprendida de un patrón inicialmente neutro porque predice consecuencias corporales. Su presencia requiere dependencia de historia y no debe confundirse con valencia primaria precargada.

## Percepción

Transformación de señales sensoriales crudas en propiedades estructuradas utilizables. Sus primitivas —por ejemplo entidad, distancia o movimiento— pueden ser decisiones de arquitectura y deben declararse como tales.

## Representación

Estado interno que conserva o transforma aspectos de información accesible al sistema para su procesamiento. No se asume que reproduzca fielmente el Ground Truth ni que tenga el significado que un observador humano le atribuye.

## Tick

Unidad discreta de orden causal y temporal de los ciclos experimentales; no equivale necesariamente a segundos. En V1 su valor absoluto pertenece a la metadata y no es accesible al agente.

## Yo

`HIPÓTESIS` Posible organización funcional y persistente de regularidades sobre estados, acciones, consecuencias e historia del mismo sistema. No se presupone como observador interno ni se entrega inicialmente mediante una etiqueta de identidad o pertenencia corporal.
