# Procedencia del desarrollo: heredado, aprendido, emergente y metadata

**Fecha:** 2026-09-15  
**Estado:** marco metodológico provisional para futuros protocolos; no fija sensores, módulos, algoritmos ni ADR-002. La arquitectura cognitiva es **PROVISIONAL — PENDIENTE DE REVISIÓN TEÓRICA Y EXPERIMENTAL**.

## Pregunta y alcance

¿Con qué nace el organismo artificial y qué tiene permitido aprender? Ante cualquier capacidad posterior: ¿proviene causalmente de su experiencia, de lo que le dimos al inicio, de una organización nueva de mecanismos simples o de información introducida por el experimento? La documentación actual no permite responder eso para todos los componentes: aún no hay agente ni parámetros iniciales definidos.

Este marco refina la misión descrita en el [informe](../PROJECT_REPORT.md), complementa la [revisión de literatura](../literature/state-of-the-art.md) y respeta [ADR-001](../decisions/ADR-001-epistemic-boundary.md). El agente no puede acceder directamente a `GroundTruthState`, tick absoluto, identidad técnica, etiquetas humanas ni metadata; `RawObservation` media toda entrada sensorial. La distinción entre señales internas y externas es un supuesto **heredado** de V1 y una fuente potencial de diseño indirecto de la autodistinción. No se modifica aquí.

La unidad de clasificación debe declararse: un **artefacto** (p. ej. una capacidad de memoria), un **contenido** (p. ej. una asociación almacenada) o una **propiedad observable** (p. ej. preferencia estable). Un módulo heredado puede alojar contenido aprendido; una propiedad candidata a emergente puede depender también de aprendizaje. Las categorías no son cuatro etiquetas excluyentes para un objeto entero. `INDUCIDO / DISEÑADO INDIRECTAMENTE` es una **bandera de auditoría transversal**, no una quinta fuente de información independiente. Si no hay evidencia causal suficiente, usar **POR DEFINIR**, no «emergente» por descarte.

## Cuatro categorías principales y una bandera de auditoría

### HEREDADO

Toda información, estructura, capacidad o predisposición **presente en `Agent(t0)` antes de su primera experiencia individual**. Su origen puede ser el diseño del investigador o una condición de inicialización, no genética real. Incluye potencialmente topología de procesamiento, plasticidad, sensores, actuadores, límites corporales, capacidad de memoria, reglas de actualización, conectividad inicial, sesgos inductivos, mecanismos temporales y restricciones homeostáticas. La clasificación exige una instantánea de t0 y descripción de quién fijó cada elemento.

**Estructura heredada ≠ conocimiento heredado.** Disponer de memoria y una regla para aprender `acción → cambio sensado` es estructura/predisposición. Inicializar una regla, peso o tabla que ya identifica `sensor_04 → peligro` es **conocimiento precargado**, aunque no aparezca la palabra «peligro». Un sesgo que hace esa asociación inevitable también merece auditoría de diseño indirecto. Una regla de supervivencia, un target de energía o una recompensa pueden ser restricciones funcionales heredadas; si codifican la respuesta de la tarea, se atribuye el éxito al diseño. Heredado no significa malo ni ilegítimo: significa que la capacidad no puede reportarse como desarrollada desde cero.

No equiparar «existía en el código» con «el agente sabía»: la regla del simulador y las anotaciones externas no son contenido cognitivo. Tampoco equiparar «estado inicial» con predisposición de especie: posiciones, energía y condiciones ambientales fijadas por el investigador son **condiciones iniciales** que pueden afectar causalmente el desarrollo, y deben declararse por separado de la arquitectura.

### APRENDIDO

Contenido o estructura interna cuya modificación **depende causalmente de la historia individual de señales, acciones y consecuencias accesibles** al agente. Asociaciones, modelos predictivos, expectativas, preferencias adquiridas, estrategias o relaciones acción–consecuencia son candidatos. Un contador, buffer o variable que cambia por tick, RNG, envejecimiento programado o actualización fija sin dependencia de observaciones relevantes no se clasifica como aprendizaje solo por variar.

La prueba mínima requiere comparar historias controladas: **experiencias diferentes → estados internos diferentes**, manteniendo herencia, estado inicial y fuentes de azar iguales o explícitamente controladas; además comprobar que la diferencia afecta la capacidad estudiada. Puede haber aprendizaje que no produzca conducta visible y conducta cambiante sin aprendizaje. Si una «preferencia adquirida» se explica completamente por una recompensa o prioridad precargada, atribuir por separado la predisposición heredada y la actualización dependiente de experiencia.

### EMERGENTE

**Definición operacional para una propiedad P y condiciones C:** P es *candidata* a emergente si (a) no existe una representación explícita de P en `Agent(t0)`; (b) P no está codificada como respuesta directa en etiquetas, recompensas, reglas o condiciones; (c) aparece reproduciblemente, bajo C, de la interacción entre mecanismos más simples y, cuando corresponda, aprendizaje; (d) puede medirse a un nivel organizativo superior al de cada regla aislada; y (e) intervenciones causales sobre interacciones o mecanismos modifican P de modo explicable. Deben predefinirse medición, C, controles y falsadores. «No lo programamos explícitamente» no satisface (b) ni (e).

Una asociación memorizada `A → B` puede ser **aprendida** sin emergencia interesante. Una organización estable que agrupe señales corporales, acciones y consecuencias como relativas al propio sistema *podría* ser candidata a emergencia si supera las pruebas anteriores; no se afirma que vaya a aparecer. La propiedad puede ser tanto aprendida como emergente, pero las pruebas responden preguntas distintas: **aprendizaje** exige dependencia causal de historia; **emergencia** exige organización no trivial e irreductibilidad explicativa frente a reglas, etiquetas y controles más simples. «Irreductibilidad explicativa» aquí no significa la integración causal Φ de IIT.

### METADATA EXPERIMENTAL

Información que usan exclusivamente investigador, simulador, evaluación o registro para reproducir y analizar corridas: `run_id`, `agent_id` técnico, tick absoluto, seed, configuración, commit, `GroundTruthState`, tipos reales, origen verdadero de sensores, etiquetas humanas, módulos activados, condición experimental y resultados objetivos. **Metadata experimental ≠ conocimiento del agente.** Como dato o etiqueta de instrumentación no puede llegar al flujo cognitivo ni influir directa o indirectamente en decisión, aprendizaje o inicialización, conforme a ADR-001 y los [contratos conceptuales](../data-contracts.md).

Hay una distinción que debe auditarse: el *registro* externo «condición A» es metadata; un sensor, cuerpo, recompensa o mecanismo configurado para A **sí afecta** al agente a través de canales autorizados y es una intervención/condición heredada o ambiental, no metadata cognitiva. Del mismo modo, registrar una seed es externo, mientras que usar un valor para generar parámetros o aleatoriedad del agente podría alterar `Agent(t0)` o su trayectoria. La documentación vigente prohíbe que **metadata** condicione la inicialización cognitiva; antes de V1 hay que especificar cómo separar el identificador/registro externo de cualquier fuente de azar causal. No se altera ADR-001 para resolver esa tensión.

### INDUCIDO / DISEÑADO INDIRECTAMENTE

Bandera para una capacidad que *parece* aprendida o emergente pero resulta facilitada, delimitada o incluso resuelta por información implícita del diseño. Pregunta obligatoria para cada hallazgo: **«¿Podría el comportamiento observado explicarse por información que introdujimos indirectamente?»** Un sesgo inductivo heredado y declarado puede ser legítimo; se vuelve problema si se omite y el resultado se atribuye enteramente a experiencia. La bandera puede ser **riesgo**, **detectado** o **descartado bajo controles especificados**; aquí solo evaluamos riesgos, sin resultados.

Fugas conceptuales a inspeccionar: nombres `internal_signals`/`external_signals`; IDs perceptivos persistentes que revelan continuidad; distancia o entidades ya segmentadas; orden fijo de canales; acciones con semántica en su nombre o sus efectos; recompensa que codifica «peligro»; ruteo corporal directo a `SelfModel`; memoria que etiqueta sucesos como «propios»; entrenamiento previo sobre la tarea final; inicialización de pesos con reglas verdaderas; valores centinela o dimensiones que revelan categorías. Hay filtración directa si entra Ground Truth/metadata prohibida; hay **diseño indirecto** aun sin filtración formal si una primitiva autorizada regala parte de la capacidad que se dice desarrollada.

## Qué está permitido aprender según la frontera vigente

ADR-001 y los contratos conceptuales permiten **investigar** cambios basados en `RawObservation`, estados perceptivos derivados, señales corporales sensadas, acciones registradas, secuencias internas, memoria y consecuencias estimadas tras nuevas observaciones. Entre los contenidos candidatos están patrones sin glosas humanas, asociaciones sensorimotoras, expectativas, modelos de regularidades, estrategias y atribución propia/externa **incierta**. «Permitido» significa que su información de origen puede ser accesible; no afirma que el agente tenga ya los módulos o pueda adquirir esos contenidos. Cada aprendizaje futuro debe conservar la cadena de procedencia.

No está permitido aprender por lectura directa de tipos/posiciones/causas verdaderas del motor, tick absoluto, ID técnico, seed, labels humanos, versión, escenario o resultado objetivo del observador. Un agente sí podría **inferir** alguna regularidad correlacionada con el mundo a partir de señales autorizadas, con error e incertidumbre medibles. Eso difiere de recibir la regla real ya resuelta. Una intervención que exponga información prohibida necesitaría revisión/versionado formal de la frontera y no pertenece al flujo cognitivo base.

## Analogía organismo–agente y límites

| Heurística biológica | Correspondencia experimental aproximada |
|---|---|
| Genética / predisposiciones de desarrollo | Arquitectura, parámetros, plasticidad y sesgos iniciales |
| Cuerpo | Sensores, actuadores y dinámica interna simulada |
| Experiencia | Historia de observaciones, acciones y consecuencias |
| Aprendizaje | Modificación dependiente de historia de estados/modelos |
| Desarrollo | Transformación del agente durante una corrida de vida individual |

### Límites de la analogía organismo-agente

No son equivalencias biológicas. Un agente simulado no trae automáticamente evolución biológica real, desarrollo embrionario, neuroplasticidad biológica, metabolismo, afecto, cuerpo físico, interacción social, escala o complejidad orgánica e historia evolutiva. Simular una variable de energía no implica metabolismo; optimizarla no implica deseo o afecto. La comparación es útil para ordenar **qué es inicial y qué cambia**, no para inferir homología ni experiencia fenomenal. Embodied cognition no es una teoría uniforme [Wilson 2002](https://doi.org/10.3758/BF03196322).

### Desarrollo individual frente a evolución generacional

El objeto inicial del proyecto es la transformación de **un mismo agente**:

```text
Agent(t0) → experiencia → Agent(t1) → experiencia → Agent(t2)
```

Evolución generacional implica variación heredable, selección y transmisión entre generaciones:

```text
Generation 1 → selección / herencia / mutación → Generation 2
```

Son escalas y mecanismos diferentes. El proyecto comienza con desarrollo individual; evolución, selección artificial y neuroevolución quedan como líneas futuras, sin algoritmos ni supuestos implementados. La distinción tiene antecedentes en robótica evolutiva [Nolfi y Floreano 2002](https://doi.org/10.1016/S1364-6613(00)01812-X) y en modelos de aprendizaje y evolución por exploración [Oudeyer y Smith 2016](https://doi.org/10.1111/tops.12196); no reivindicamos originalidad. Pregunta futura: **¿qué propiedades conviene heredar y cuáles conviene dejar aprendibles?**

## «Nacimiento» experimental: `Agent at t0`

`t0` es la instantánea **antes de la primera `RawObservation` y antes de cualquier actualización dependiente de experiencia**. Si hay precalibración, preentrenamiento, experiencias de inicialización o «warm-up», deben contarse como historia previa y declararse; no pueden ocultarse bajo t0. Tampoco se presupone que `InitialKnowledge` sea vacío: debe enumerarse y justificarse. No se crean clases Python.

| Parte del manifiesto t0 | Pregunta documental |
|---|---|
| `InitialArchitecture` | ¿Qué conexiones, operadores, rutas y permisos de lectura existen? |
| `InitialParameters` | ¿Qué pesos, umbrales, tasas, capacidades, tablas y constantes están fijados? ¿Por quién? |
| `InitialInternalState` | ¿Qué memoria, variables, activaciones, buffers y estados se inicializan? |
| `InitialKnowledge` | ¿Qué asociaciones, categorías, modelos o políticas contienen información antes de observar? Incluso implícita. |
| `InitialBiases` | ¿Qué sesgos inductivos, asimetrías de canal, objetivos y restricciones orientan el aprendizaje? |
| `InitialBody` | ¿Qué límites, dinámica interna, sensores y actuadores tiene el cuerpo simulado? |

Para reconstruir «qué sabía y qué podía hacer» hay que registrar por separado **contenido cognitivo inicial**, **capacidades potenciales** y **entorno/condición inicial**. La identidad técnica del cuerpo pertenece al simulador/metadata; el agente no recibe «este cuerpo soy yo». Registrar la snapshot t0 como traza del observador no autoriza al agente a leerla completa. Capacidades que ya se observan en ensayos sin aprendizaje deben atribuirse a la herencia/condición inicial, aunque el agente luego las refine.

## Desarrollo como transformación causal

```text
InitialArchitecture + InitialParameters + InitialInternalState
                 + InitialBody + experiencia individual
                         → estado desarrollado del agente
```

La historia debe ser causalmente relevante para afirmar aprendizaje. **PREDICCIÓN, no garantía:** dos agentes con arquitectura, parámetros y estado t0 idénticos pero historias diferentes *podrían* desarrollar estados internos y políticas diferentes si el mecanismo permite aprendizaje dependiente de experiencia. Si no divergen, podría faltar plasticidad pertinente, las historias podrían ser funcionalmente equivalentes o la métrica podría no medir el cambio; hay que predefinir esas alternativas. **Control contrario:** con arquitectura, parámetros, estado, cuerpo, historia y azar idénticos, las trazas deberían reproducirse salvo fuentes de no determinismo declaradas. Diferencias inexplicadas impiden atribuir causalmente una capacidad a la historia.

La transformación no demuestra emergencia: un script puede actualizar una tabla exactamente según experiencia. Tampoco toda divergencia constituye individualidad cognitiva: ruido en una salida puede producir distintas acciones sin modelos internos distintos. Comparar trazas de `RawObservation`, `PerceivedState`, `PatternState`, memoria, modelos, predicciones, `Decision` y `Outcome` desde la vista del investigador, manteniendo la barrera de ADR-001.

## Matriz provisional de procedencia

Los valores describen **lo permitido o previsto por documentación**, no una implementación. `SÍ` en heredado suele referirse a la existencia de una interfaz/capacidad, nunca automáticamente a su contenido. `POR DEFINIR` evita inventar una configuración t0. La columna «riesgo» usa `SÍ` cuando la documentación ya señala un canal concreto de inducción y `PARCIAL` cuando depende de detalles aún no fijados. `NO APLICA` en emergencia marca infraestructura cuya existencia no sería una propiedad emergente interesante.

| Elemento | Heredado | Aprendible | Emergente candidato | Riesgo de diseño indirecto | Estado actual |
|---|---|---|---|---|---|
| Sensores | SÍ: canales/capacidad | POR DEFINIR: calibración | NO APLICA: existencia | SÍ: modalidad, orden, etiquetas internal/external | Separación V1 en ADR-001; contratos concretos pendientes |
| Actuadores | SÍ: repertorio/límites | POR DEFINIR: calibración | NO APLICA: existencia | PARCIAL: nombres/efectos de acción | Repertorio no definido |
| Mecanismos de aprendizaje | POR DEFINIR: predisposición | POR DEFINIR: plasticidad de la regla | NO APLICA: mera existencia | SÍ si regla codifica solución | Sin algoritmo ni t0 definidos |
| Memoria | POR DEFINIR: capacidad inicial | SÍ: contenido posible | NO APLICA: capacidad; POR DEFINIR: organización | PARCIAL: etiquetas «propio», tick encubierto | `MemoryRecord` conceptual |
| `PerceivedState` | PARCIAL: primitivas permitidas | POR DEFINIR: transformación adaptable | NO: primitivas heredadas; POR DEFINIR: estructuras nuevas | SÍ: entidad, distancia, movimiento | Contrato conceptual vigente |
| `PatternState` | POR DEFINIR: formato y priors | SÍ: patrones previstos como aprendidos | POR DEFINIR: organización de patrones | PARCIAL: glosas, IDs, recompensas | No existe aprendizaje implementado |
| `WorldModel` / `InternalModel` | POR DEFINIR: mecanismo/priors | SÍ: contenido previsto | POR DEFINIR | SÍ si reglas/preentrenamiento anticipan mundo | Arquitectura provisional |
| `Prediction` | POR DEFINIR: predictor | SÍ: expectativas posibles | NO APLICA: predicción aislada | PARCIAL: futuro filtrado o horizonte impuesto | Contrato conceptual |
| `IntegratedState` | POR DEFINIR: operación | POR DEFINIR: contenido dinámico | POR DEFINIR: organización superior | SÍ si reúne explícitamente «presente/self» | No equivale a indicador de consciencia |
| `SelfModel` / `SelfState` | POR DEFINIR: estructura | SÍ: regularidades previstas | POR DEFINIR: autodistinción | SÍ: ruteo de señales corporales/acciones | Identidad técnica prohibida en ADR-001 |
| `Valuation` | POR DEFINIR: función/objetivos | POR DEFINIR: preferencias adquiridas | POR DEFINIR | SÍ si recompensa trae «peligro»/solución | Valor funcional, no afecto |
| `Decision` | POR DEFINIR: selector | POR DEFINIR: política | NO APLICA: selección aislada | PARCIAL: alternativas y nombres de acciones | Contrato conceptual |
| Acciones concretas | POR DEFINIR: repertorio inicial | POR DEFINIR: elección/estrategia | POR DEFINIR: patrón conductual | PARCIAL: semántica del repertorio | No definido |
| Preferencias | POR DEFINIR: objetivos iniciales | POR DEFINIR | POR DEFINIR: organización estable | SÍ: utilidad/recompensa precargada | No confundir con deseo |
| Representación temporal | PARCIAL: orden/latencia posible | SÍ: secuencias previstas | POR DEFINIR | SÍ: tick absoluto/contador alias | Tick global solo metadata |
| Distinción self/world | PARCIAL: cuerpo y canales separados | POR DEFINIR | POR DEFINIR | SÍ: internal/external y acciones propias | Pregunta experimental, no resultado |
| Body model/schema | POR DEFINIR | POR DEFINIR | POR DEFINIR | SÍ si geometría corporal se precarga | Candidato ausente en arquitectura actual |
| Atención | POR DEFINIR | POR DEFINIR | POR DEFINIR | PARCIAL: prioridad fijada por diseño | Mecanismo posible, no congelado |
| Recurrencia | POR DEFINIR | POR DEFINIR | POR DEFINIR | PARCIAL: rutas de feedback heredadas | No definida temporalmente |
| Global workspace / broadcast | POR DEFINIR | POR DEFINIR | POR DEFINIR | PARCIAL: difusión concedida por diseño | No equivale a `IntegratedState` |
| Metarrepresentación | POR DEFINIR | POR DEFINIR | POR DEFINIR | SÍ si estados de orden superior precargados | No definida |

Una arquitectura puede ser heredada y legítima como **predisposición**; el contenido que adquiera en ella exige prueba de historia. Para propiedades candidatas como self/world, registrar ambas capas y la posible bandera de diseño indirecto. La matriz debe actualizarse **antes** de cualquier protocolo V1 cuando existan t0, campos, reglas y sensores especificados, sin convertir sus valores provisionales en decisiones de arquitectura.

**Lectura de conocimiento precargado hoy:** no hay pesos, tablas o reglas cognitivas implementadas, así que no se puede afirmar que un `WorldModel`, `SelfModel` o patrón concreto ya contenga conocimiento inicial. Sí hay **contenido estructural preconfigurado** en la propuesta documental: origen internal/external de canales, primitivas posibles de entidad/distancia/movimiento en `PerceivedState`, ruteo del cuerpo por el simulador y disponibilidad de acciones propias registradas. Esas pistas pueden acortar el aprendizaje de categorías, temporalidad y autodistinción. Sensores, capacidad de memoria, plasticidad y límites corporales serían predisposiciones heredadas legítimas **si se declaran y no se atribuyen como capacidades desarrolladas**. Recompensas, objetivos, topologías y priors concretos permanecen por definir; no deben clasificarse como conocimiento inocuo antes de auditarlos.

## Criterio para afirmar «esta capacidad se desarrolló»

La afirmación debe acotar una capacidad y satisfacer, con medidas predefinidas, al menos estas diez condiciones:

1. **Ausencia en t0:** ni la capacidad funcional ni una política/tablas que ya la realizan están presentes bajo controles sin experiencia.
2. **Aparición tras experiencia relevante:** registrar primer momento observable y oportunidad de aprendizaje.
3. **Dependencia de historia:** variar experiencias manteniendo herencia, inicialización y azar controlados; trazar el cambio interno.
4. **Generalización:** probar casos nuevos separados de la experiencia, no solo recuerdo de episodios.
5. **Persistencia suficiente:** fijar horizonte antes de medir; descartar fluctuación de un tick.
6. **Reproducibilidad estadística:** múltiples corridas/seeds y variación explícita, sin elegir ejemplos llamativos.
7. **Intervención causal:** alterar mecanismo o contenido aprendido y observar la predicción de cambio, con controles de capacidad general.
8. **Control más simple:** comparar agente reactivo, regla local, memoria fija o predictor simple según la capacidad.
9. **Sin filtración semántica razonable:** auditar primitivas, ruteo, recompensa, nombres, IDs y entrenamiento previo; un resultado que depende de esas pistas no es «desde cero».
10. **Trazabilidad:** reconstruir cadena de señales autorizadas → estados modificados → decisión/consecuencia, sin usar metadata como entrada.

**Aparición** es detectar una conducta; **aprendizaje** es demostrar dependencia causal de experiencia; **generalización** es transferencia a casos nuevos; **emergencia** requiere además la prueba organizativa definida arriba. Ninguna de estas etiquetas implica experiencia fenomenal. Si una condición no se puede evaluar, informar «capacidad observada; origen por definir» y no una versión debilitada de «emergió».

## Information Provenance Audit

Para **cada variable legible por un módulo del agente**, y también para cada ruta entre variables, registrar antes de implementar:

| Pregunta obligatoria | Evidencia que debe quedar documentada |
|---|---|
| 1. ¿Quién la creó? | Sensor, módulo, actuador, inicializador, motor o investigador; propietario del flujo. |
| 2. ¿De qué información deriva? | Padres de la transformación y cadena hasta señal sensada/estado autorizado. |
| 3. ¿Qué semántica contiene? | Unidades, nombre, segmentación, categoría implícita, significado asignado por diseño. |
| 4. ¿Estaba disponible en t0? | Valor inicial, constante, prior, buffer o posibilidad de lectura antes de experiencia. |
| 5. ¿Puede revelar Ground Truth? | Ruta directa, correlato perfecto, tipo/posición/causa real o regla del mundo. |
| 6. ¿Puede revelar identidad? | ID técnico, continuidad, cuerpo «propio», ruteo identificable o canal dedicado. |
| 7. ¿Puede revelar categorías humanas? | Labels, recompensas, nombres, orden, dimensiones o valores centinela. |
| 8. ¿Puede revelar la respuesta esperada? | Tarea final codificada en prior, recompensa, configuración o entrenamiento. |
| 9. ¿Qué módulos pueden leerla? | Dependencias y permisos declarados; rutas laterales indirectas. |
| 10. ¿Puede influir causalmente en decisión? | Camino a `Decision`, aprendizaje, atención o inicialización; controles de bloqueo. |

Propuesta documental para futuros contratos, **sin modificarlos ahora**: campo de procedencia por variable/ruta que registre origen, padres autorizados, momento de disponibilidad, semántica diseñada, lectores, destino causal, condición experimental y prueba de no filtración. El observador puede unir trazas y Ground Truth para auditar; esa unión nunca pasa al agente. El análisis debe incluir canales indirectos por recompensa, inicialización, valores por defecto y orden estable. Una regla formal de acceso no basta para probar ausencia de inducción conceptual.

## Cinco experimentos conceptuales, no congelados

| Experimento | Intervención y control | Pregunta / lectura limitada |
|---|---|---|
| **A — misma herencia, distinta experiencia** | Igual t0 y azar controlado; historias contrastadas con oportunidad de aprendizaje equivalente. | ¿Qué estados y conductas divergen por historia? La divergencia sola no prueba emergencia. |
| **B — misma herencia, misma experiencia** | Igual t0, observaciones, acciones cuando sean controladas y seed/fuentes de azar. | ¿Hay divergencia sin fuente causal identificable? Control de reproducibilidad. |
| **C — distinta herencia, misma experiencia** | Cambiar un único mecanismo/parametrización inicial; igual historia sensorial cuando sea posible. | ¿Qué capacidad depende de esa predisposición? Cambiar herencia puede cambiar experiencias posteriores: declarar ese mediador. |
| **D — información semántica oculta** | Comparar canales neutrales con estructurados/semánticos; controlar información efectiva y tarea. | ¿Cuánto rendimiento o autodistinción se explica por primitivas/labels de diseño? No llamar «neutral» a un canal sin auditarlo. |
| **E — self/world** | Comparar clasificación internal/external, canales neutrales y grados de información acción–consecuencia. | ¿Qué parte de autodistinción fue aprendida y qué parte entregó el ruteo? Comparar modelos internos, no solo conducta. |

**Límite de ADR-001:** V1 exige señales internas y externas distinguibles por arquitectura. Las condiciones D/E con canales neutralizados o sin identificación son **contrafactuales metodológicos futuros**; si contradicen esa condición aceptada, necesitarán nuevo ADR o versión/intervención formal antes de ejecutarse. Etiquetas semánticas, Ground Truth e identidad técnica tampoco pueden introducirse en el flujo cognitivo base. Un brazo experimental que exponga información prohibida tendría que quedar separado, versionado y justificado; esta lista no lo autoriza.

## Capacidades análogas a comportamientos humanos: lenguaje controlado

Se pueden estudiar, progresivamente y sin garantizar aparición, exploración, habituación, anticipación, aprendizaje por consecuencias, memoria, preferencias, aversión funcional, adaptación, generalización, curiosidad operacionalizada, self/world funcional, agencia, reconocimiento de otros agentes, imitación, cooperación, competencia y comunicación. Cada término requiere conducta y métrica operacionales. Una mención de miedo, dolor, deseo, intención o curiosidad sin especificación funcional y controles es **INTERPRETACIÓN ANTROPOMÓRFICA**, no descripción de estado cognitivo.

| Observación | DESCRIPCIÓN FUNCIONAL permitida | INTERPRETACIÓN ANTROPOMÓRFICA injustificada |
|---|---|---|
| El agente elige con mayor frecuencia acciones que mantienen una variable corporal sensada en un rango, en escenarios nuevos. | Preferencia funcional por un rango bajo el mecanismo/objetivo definido; evaluar si el objetivo era heredado. | «Quiere sobrevivir», «siente miedo», «sufre» o «tiene deseo». |
| Explora entradas con alta incertidumbre y cambia su política tras observar consecuencias. | Muestreo dirigido por una medida de incertidumbre definida; verificar dependencia de historia. | «Tiene curiosidad» sin operacionalizarla. |
| Diferencia cambios tras acciones registradas y perturbaciones externas. | Autodistinción funcional bajo control de ruteo y pistas de canal. | «Sabe que es él mismo» o «tiene experiencia de ownership». |

La similitud conductual con humanos no implica equivalencia biológica, identidad de mecanismo ni fenomenología.

## Falsadores del enfoque de desarrollo

Resultados futuros que obligarían a debilitar **afirmaciones concretas**:

- Una capacidad supuestamente desarrollada aparece igual en t0 o sin aprendizaje: atribuirla a herencia/diseño.
- Un agente reactivo o reglas locales producen el mismo comportamiento y estados candidatos: revisar la necesidad de mecanismos complejos.
- Ablar memoria no cambia dependencia de historia: revisar la hipótesis sobre memoria, o detectar otro almacenamiento.
- Historias diferentes no producen diferencias internas relevantes bajo controles: debilita esa predicción de plasticidad.
- Neutralizar pistas semánticas hace desaparecer conductas complejas: atribuir el efecto a diseño indirecto hasta probar otra explicación.
- Self/world funcional solo aparece con clasificación internal/external: debilita emergencia de una frontera aprendida en esa arquitectura.
- El agente memoriza ejemplos sin generalizar: reportar aprendizaje de casos, no desarrollo de capacidad general.
- El rendimiento depende de recompensas que ya codifican la solución: atribuir al diseño el objetivo/semántica.
- Resultados no se reproducen o hay divergencia B inexplicada: no inferir dependencia causal limpia.
- Cada nueva capacidad requiere una regla manual específica: debilita una tesis de desarrollo abierto por mecanismos iniciales generales.

Un resultado negativo se preserva. No se reformula retrospectivamente la capacidad o la emergencia para declarar éxito. Los controles deben evitar que una ablación cause un déficit trivial por pérdida de entradas, tiempo de cómputo o capacidad general.

## Desarrollo cognitivo no equivale automáticamente a consciencia

El organismo artificial podría aprender, desarrollar preferencias, construir `WorldModel`, diferenciar consecuencias de acciones, distinguir self/world, adaptarse y mostrar historia individual sin que eso demuestre experiencia fenomenal. Son resultados funcionales; algunas organizaciones podrían luego compararse con indicadores derivados de teorías, según los niveles A/B/C de la [revisión del estado del arte](../literature/state-of-the-art.md#qué-contaría-como-evidencia). La consciencia no debe usarse para explicar una conducta cuando un mecanismo computacional más simple la explica. Un indicador B tampoco convierte automáticamente un resultado en afirmación C.

Tres objetivos ordenan el trabajo: **(1) desarrollo cognitivo artificial:** eventualmente construir un agente mínimo que adquiera capacidades mediante interacción, con conocimiento semántico humano precargado solo si se declara como condición experimental; **(2) descomposición causal:** comparar herencia, experiencias, intervenciones y controles para atribuir capacidades; **(3) relación con consciencia:** contrastar posteriormente organizaciones resultantes con teorías e indicadores científicos, sin inferir fenomenología por conducta. Esta secuencia describe un programa de investigación, no un compromiso de implementar la lista modular actual.

## Antecedentes y límites de originalidad

La distinción entre predisposición, historia sensorimotora y desarrollo tiene **antecedentes fuertes** en developmental robotics y aprendizaje de body schema/active self [Hoffmann et al. 2010](https://doi.org/10.1109/TAMD.2010.2086454), [Nguyen et al. 2021](https://doi.org/10.1007/s13218-021-00703-z). La dependencia cuerpo–entorno y de historia tiene antecedentes en [embodied cognition](https://doi.org/10.3758/BF03196322) y [sensorimotor contingencies](https://doi.org/10.1017/S0140525X01000115). La diferencia entre aprendizaje individual y evolución de predisposiciones tiene antecedentes en robótica evolutiva y aprendizaje exploratorio [Nolfi y Floreano 2002](https://doi.org/10.1016/S1364-6613(00)01812-X), [Oudeyer y Smith 2016](https://doi.org/10.1111/tops.12196). La [revisión previa](../literature/state-of-the-art.md) ya registra que self/world aprendido, modelos internos y ablaciones no son ideas inéditas. Aquí se propone **trazabilidad local de procedencia** para este proyecto, no una teoría original del desarrollo o de la consciencia. Para afirmaciones específicas de *artificial life* o neuroevolución más allá de esa distinción: **VERIFICACIÓN PENDIENTE**; esta tarea no realiza una revisión exhaustiva de esas áreas.

## Tensiones y afirmaciones todavía no justificadas

1. ADR-001 separa canales internos/externos y conoce la frontera física para ruteo. La autodistinción no puede describirse como «completamente emergente» sin controlar cuánto aporta esa predisposición. El contrato permite información corporal percibida y acciones registradas: fuentes legítimas, pero potentes.
2. `PerceivedState` puede traer entidad, distancia, dirección y movimiento por diseño. No está justificado describir todo aprendizaje posterior como «desde señales no semánticas» sin cuantificar esas primitivas.
3. El informe llama aprendidos a `PatternState` y algunas regularidades de `SelfState`, pero no existe `Agent(t0)`, algoritmo, contenido inicial ni prueba de dependencia de historia. Son **objetivos/contratos**, no capacidades ya aprendidas.
4. `IntegratedState` reúne información y `SelfState` tiene ruta corporal prevista. No está justificado que esas estructuras produzcan consciencia, emergencia o siquiera una autodistinción aprendida.
5. Los protocolos piden registrar seed/configuración; ADR-001 prohíbe que metadata influya en inicialización cognitiva. Debe documentarse la diferencia entre **registro externo** y **parámetro causal**, especialmente si se usa RNG. No se resuelve aquí.
6. No existe una definición operacional de homeostasis, recompensa, preferencias, atención, recurrencia, workspace, metarrepresentación ni capacidad social; atribuirles efectos sería especulación.
7. No está justificado afirmar que un agente mínimo reproduzca desarrollo biológico o posea fenomenología; la analogía tiene los límites anteriores.

## Estado de decisiones y preguntas para V1

| Estado | Contenido |
|---|---|
| **CONGELADO** | ADR-001 aceptado: frontera Ground Truth → sensores → cognición; Ground Truth y metadata inaccesibles al agente; tick absoluto e identidad técnica externos. La necesidad metodológica de atribuir lo diseñado frente a lo adquirido guía esta tarea, **sin convertirse en nuevo ADR**. |
| **PROVISIONAL** | Módulos cognitivos, sensores concretos y estructura perceptiva, mecanismos de aprendizaje, `SelfModel`, `WorldModel`, `Valuation`, atención, recurrencia, workspace y metarrepresentación. |
| **ABIERTO** | Qué heredar, aprender o intentar medir como emergencia; arquitectura mínima; indicadores de desarrollo y relación posterior con indicadores de consciencia. |

Antes de implementar V1 hay que responder: ¿qué contiene exactamente `Agent(t0)`?, ¿qué priors y conocimiento quedan precargados?, ¿qué campos/permisos permiten pistas de identidad o semántica?, ¿cómo separar seed de registro y azar causal?, ¿qué funciones de recompensa/objetivos se heredan?, ¿qué experiencia puede cambiar qué estado?, ¿qué capacidad y generalización se medirá primero?, ¿qué controles reactivos y de no aprendizaje se requieren?, ¿qué intervención D/E es compatible con ADR-001 y cuál exigiría revisión formal?, ¿qué resultado refutaría cada afirmación? No se escoge ahora la arquitectura que responderá esas preguntas.
