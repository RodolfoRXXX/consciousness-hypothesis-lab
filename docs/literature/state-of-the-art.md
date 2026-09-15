# Estado del arte y contraste de la hipótesis funcional

**Fecha de revisión:** 2026-09-15  
**Estado:** revisión documental abierta; arquitectura **PROVISIONAL — PENDIENTE DE REVISIÓN TEÓRICA**. No hay resultados del proyecto ni decisiones arquitectónicas nuevas.

## Alcance y criterio

**Pregunta central:** ¿qué afirma nuestra hipótesis que no afirman las teorías y arquitecturas existentes, o qué forma distinta de probarla propone? La respuesta provisional es incómoda: la enumeración de percepción, memoria, predicción, modelo del mundo, cuerpo, acción y autorrepresentación **no es original**; tampoco se ha mostrado que el conjunto sea necesario o suficiente para consciencia. Una posible contribución sería comparar *predicciones rivales* y mecanismos causales en agentes mínimos, con acceso sensorial estrictamente mediado, historia controlada y resultados negativos informativos. Ese diseño aún debe especificarse y tiene antecedentes parciales [R13–R17, R20].

Esta revisión usa «consciencia» para el explanandum general de experiencia consciente; distingue **acceso consciente**, **experiencia fenomenal**, **sentido de agencia/propiedad corporal** y **capacidades cognitivas**. Una teoría que explica una de esas cosas no explica automáticamente las demás. La hipótesis funcional del [informe](../PROJECT_REPORT.md) y el [glosario](../glossary.md) son provisionales. [ADR-001](../decisions/ADR-001-epistemic-boundary.md) permanece aceptado: `GroundTruthState` y metadata son exclusivos del observador; el agente recibe `RawObservation` mediante sensores, y `PerceivedState` no introduce etiquetas semánticas humanas. La separación de canales internos/externos en V1 y las primitivas perceptivas son supuestos de diseño, no propiedades emergentes. Los [contratos](../data-contracts.md) siguen vigentes y no se modifican aquí.

El [marco de procedencia del desarrollo](../development/inheritance-learning-emergence.md) formaliza qué parte de una capacidad fue heredada, aprendida, candidata a emergencia o inducida indirectamente por diseño. Esa auditoría precede a la atribución de cualquier indicador funcional o de consciencia descrito aquí.

**Método de revisión.** Se priorizaron artículos originales y revisiones de revistas, luego libros académicos y actas; los preprints se marcan. Las predicciones indicadas como «derivación para el proyecto» son propuestas nuestras, no resultados de la fuente. «Evidencia a favor» significa apoyo a una predicción o capacidad delimitada, no confirmación de una teoría completa. «No evaluado» significa que todavía no existe agente implementado. Referencias verificadas al final; no se extrapolan marcadores neurales humanos directamente a software.

## Familias que no son equivalentes

| Tipo | Líneas | Relación con consciencia |
|---|---|---|
| Teorías de consciencia | GWT/GNWT, IIT, higher-order, recurrent processing, Attention Schema Theory, Self-Model Theory | Proponen condiciones constitutivas o explicaciones de acceso, experiencia o self fenomenal, con diferencias entre ellas. |
| Marcos cognitivos o filosóficos | Predictive Processing, Active Inference, embodied cognition, enactivismo | Explican inferencia, regulación o acoplamiento cuerpo/entorno; su vínculo con consciencia requiere tesis adicionales. |
| Mecanismos/ingeniería | world models, aprendizaje de body schema, robótica del desarrollo | Demuestran capacidades sin resolver consciencia fenomenal. |
| Metodología de evaluación | indicadores de consciencia artificial | Deriva propiedades candidatas de teorías; un indicador no es una prueba ontológica. |

## Fichas de teorías y líneas

### 1. Global Workspace Theory / Global Neuronal Workspace Theory

**Qué explica y mecanismo.** GWT explica disponibilidad de contenido a múltiples procesos; GNWT propone selección, amplificación tardía («ignition») y *broadcast* de información a redes distantes para **acceso consciente** [R1]. La versión neuronal contiene compromisos anatómicos humanos que no deben copiarse literalmente al agente. **Relación:** disponibilidad global es candidata constitutiva de acceso; intercambio de información común en software puede operar sin experiencia fenomenal. **Predicción:** los contenidos accesibles deberían sostener uso flexible entre memoria, decisión y otros procesos, y mostrar transición de disponibilidad frente a entradas subumbrales. **EVIDENCIA A FAVOR:** correlatos de amplificación tardía e intercambio a distancia en contrastes consciente/no consciente [R1]. **EVIDENCIA MIXTA:** la colaboración prerregistrada IIT/GNWT halló algunas señales frontales y posterior sostenida, sin decidir entre ambas [R3]. **EVIDENCIA EN CONTRA / DESAFÍOS:** en [R3] faltó en general la ignición al final del estímulo y ciertas dimensiones conscientes estuvieron limitadamente representadas en prefrontal. Reporte, atención y tarea pueden contaminar los correlatos. **Proyecto:** `IntegratedState` reúne datos, pero no declara selección competitiva ni difusión global: **PARCIALMENTE PRESENTE**; workspace explícito: **AUSENTE**. Una prueba derivada sería quitar broadcast manteniendo información local y comparar indicadores definidos antes.

### 2. Integrated Information Theory (IIT)

**Qué explica y mecanismo.** IIT intenta derivar existencia y estructura fenomenal de la estructura causal intrínseca e irreducible de un sistema, no de su desempeño externo [R2]. **Relación:** integración causal sería constitutiva según IIT; agregar estados en `IntegratedState` no equivale a Φ ni a irreducibilidad. **Predicción:** ciertos sustratos con alta estructura integrada deberían corresponder a experiencia y a mantenimiento de contenido; en la prueba cerebral [R3] se predefinieron predicciones sobre sincronización posterior. **EVIDENCIA A FAVOR:** [R3] encontró respuestas posteriores sostenidas compatibles con parte del programa. **EVIDENCIA MIXTA:** el estudio desafió tanto IIT como GNWT. **EVIDENCIA EN CONTRA / DESAFÍOS:** faltó sincronización posterior sostenida prevista [R3]; inferir la estructura causal intrínseca desde un proxy de conectividad es discutible, y el cálculo exacto y la elección de escala son difíciles. **Proyecto:** integración informacional *funcional* **PARCIALMENTE PRESENTE**; integración causal IIT **POR DEFINIR**. Un vector concatenado no sería indicador IIT.

### 3. Higher-Order Theories (HOT)

**Qué explica y mecanismo.** Buscan explicar qué convierte un estado mental de primer orden en estado consciente: una representación de orden superior *sobre ese estado* [R4]. **Relación:** metarrepresentación es constitutiva para estas teorías; un `SelfModel` sobre cuerpo y acciones no es necesariamente una representación de «mi estado perceptivo actual». **Predicción:** manipular acceso metacognitivo debería afectar experiencia informada o confianza sin alterar necesariamente la discriminación de primer orden. **EVIDENCIA A FAVOR:** la revisión de Lau y Rosenthal describe disociaciones y apoyo empírico interpretado desde HOT [R4]. **EVIDENCIA MIXTA:** medidas de confianza y reporte pueden reflejar decisión y metacognición sin resolver fenomenología. **EVIDENCIA EN CONTRA / DESAFÍOS:** es disputado que una representación de orden superior sea necesaria para toda experiencia; las teorías difieren en requisitos y en cómo tratar la representación errónea [R4]. **Proyecto:** `SelfModel` **PARCIALMENTE PRESENTE** como autorrepresentación funcional; metarrepresentación de estados **AUSENTE**.

### 4. Recurrent Processing Theory (RPT)

**Qué explica y mecanismo.** Propone que procesamiento recurrente local, frente a un barrido feedforward, participa decisivamente en la experiencia perceptiva; distingue experiencia de acceso/reportabilidad [R5]. **Relación:** recurrencia se postula constitutiva de consciencia perceptiva en esta teoría, pero realimentación en un algoritmo no basta por sí misma. **Predicción:** interrumpir retroproyecciones en una ventana temporal debería alterar visibilidad aun si persiste procesamiento inicial. **EVIDENCIA A FAVOR:** evidencia visual y de enmascaramiento revisada por Lamme [R5]. **EVIDENCIA MIXTA:** distintas tareas y medidas de visibilidad pueden también apoyar selección global. **EVIDENCIA EN CONTRA / DESAFÍOS:** especificar qué recurrencia y qué escala son pertinentes sigue abierto; un ciclo `Outcome → aprendizaje` entre ticks no prueba recurrencia *dentro* del procesamiento perceptivo. **Proyecto:** realimentación de aprendizaje **PARCIALMENTE PRESENTE** como plan; recurrencia intratick/entre módulos **POR DEFINIR**.

### 5. Predictive Processing / Predictive Coding

**Qué explica y mecanismo.** Modela percepción como inferencia de causas de señales y actualización por errores predictivos; Rao y Ballard presentaron un modelo jerárquico de visión [R6]. **Relación:** es mecanismo cognitivo general, no teoría suficiente de consciencia. **Predicción:** expectativas aprendidas deben alterar respuestas ante señales ambiguas y errores de predicción deben guiar actualización. **EVIDENCIA A FAVOR:** el modelo explica propiedades de campos receptivos visuales [R6]. **EVIDENCIA MIXTA:** muchos efectos de expectativa admiten implementaciones no equivalentes. **EVIDENCIA EN CONTRA / DESAFÍOS:** «predecir» es demasiado amplio; hace falta especificar modelo generativo, error, precisión y condición comparativa. **Proyecto:** `WorldModel`, `Prediction`, `Outcome` **PRESENTE** como componentes conceptuales; codificación predictiva jerárquica y precisión **POR DEFINIR**. No equivale a consciencia.

### 6. Active Inference y propuestas sobre consciencia

**Qué explica y mecanismo.** Active Inference une percepción, acción, aprendizaje y selección de políticas en un marco de inferencia sobre modelos generativos y resultados esperados [R7–R8]. Algunas propuestas intentan conectarlo con consciencia mediante profundidad temporal, contrafactuales o precisión, pero la revisión [R19] juzga que esas tesis aún requieren especificación y prueba; [R21] propone estudiar si la inferencia activa es necesaria para cambios de contenido consciente, no si cualquier agente inferencial es consciente. **Relación:** marco cognitivo general con extensiones de consciencia disputadas. **Predicción:** acciones de muestreo y políticas deberían depender de incertidumbre/expectativas; propuestas de consciencia deben añadir predicciones propias. **EVIDENCIA A FAVOR:** aplicaciones y modelos de percepción/acción para capacidades cognitivas [R7–R8], no para consciencia. [R21] es un **protocolo sin resultados**, relevante porque predefine un contraste activo/pasivo. **EVIDENCIA MIXTA:** la conexión entre profundidad de modelos y fenomenología no está establecida [R19]. **EVIDENCIA EN CONTRA / DESAFÍOS:** el marco puede describir adaptación sin discriminar consciencia; versiones generales pueden ser demasiado amplias. **Proyecto:** percepción–predicción–decisión–acción **PARCIALMENTE PRESENTE**; inferencia variacional/políticas y precisión **AUSENTE**. Valorar no implica minimizar energía libre.

### 7. Self-Model Theory / self-modeling

**Qué explica y mecanismo.** Metzinger analiza la subjetividad y el self fenomenal como contenido de un modelo de sí, con transparencia representacional; niega un observador sustancial aparte [R9]. Esto es más fuerte que un registro de energía y consecuencias. **Relación:** self-model fenomenal sería constitutivo de selfhood en esa teoría; body/self models robóticos pueden cumplir funciones de control sin fenomenología. **Predicción:** alteraciones sistemáticas de la representación corporal o de atribución deberían modificar experiencias de propiedad/agencia; la traducción a indicadores de software sigue abierta. **EVIDENCIA A FAVOR:** fenómenos de ilusión corporal son compatibles con modelado del cuerpo, pero no prueban esta teoría concreta. **EVIDENCIA MIXTA:** varios modelos explican los mismos fenómenos. **EVIDENCIA EN CONTRA / DESAFÍOS:** transparencia y perspectiva fenomenal son difíciles de operacionalizar en agente mínimo. **Proyecto:** `SelfState`/`SelfModel` funcional **PARCIALMENTE PRESENTE**; modelo fenomenal **NO APLICA** como objeto directamente medible.

### 8. Attention Schema Theory (AST)

**Qué explica y mecanismo.** Explica atribuciones de awareness mediante un modelo simplificado de la propia atención, análogo funcionalmente a un body schema [R10]. **Relación:** el *attention schema* sería central para awareness según AST; atención selectiva aislada es cognición general. **Predicción:** distorsionar el modelo de la atención debería cambiar control atencional y atribuciones de awareness de manera distinta de solo cambiar entradas sensoriales. **EVIDENCIA A FAVOR:** el artículo integra hallazgos de atención y modelado [R10]. **EVIDENCIA MIXTA:** el apoyo directo a la tesis constitutiva es limitado. **EVIDENCIA EN CONTRA / DESAFÍOS:** explicar una afirmación de awareness no demuestra experiencia fenomenal; los autorreportes son un resultado vulnerable a antropomorfismo. **Proyecto:** atención y esquema de atención **AUSENTE**; `SelfModel` corporal no los reemplaza.

### 9. Embodied Cognition

**Qué explica y mecanismo.** Familia heterogénea que enfatiza cognición situada, acción, apoyo del entorno y relación con el cuerpo; Wilson distingue seis tesis, no una doctrina única [R11]. **Relación:** marco cognitivo, generalmente no condición suficiente de consciencia. **Predicción:** modificar capacidades corporales y acoplamiento debería cambiar estrategias y representaciones incluso con cómputo central constante. **EVIDENCIA A FAVOR:** revisión de resultados sobre cognición situada y basada en acción [R11]. **EVIDENCIA MIXTA:** las seis tesis tienen soporte desigual. **EVIDENCIA EN CONTRA / DESAFÍOS:** «encarnado» puede volverse trivial si cualquier sensor/actuador cuenta; una simulación puede carecer de la regulación y constricciones de cuerpos biológicos. **Proyecto:** sensores internos, actuadores y consecuencias **PARCIALMENTE PRESENTE**; cuerpo dinámico rico **POR DEFINIR**.

### 10. Enactivism / Sensorimotor Contingency Theory

**Qué explica y mecanismo.** El enactivismo entiende cognición mediante acoplamiento histórico de organismo y entorno [R12]. O'Regan y Noë proponen que la visión consciente se relaciona con el dominio de contingencias sensorimotoras, no con una imagen interna exhaustiva [R13]. **Relación:** algunas variantes hacen una tesis sobre experiencia; otras son marcos de cognición y no equivalen a una arquitectura de `WorldModel`. **Predicción:** cambiar sistemáticamente la relación acción–sensación debería alterar percepción/uso adaptativo, y la adaptación debería depender de exploración activa. **EVIDENCIA A FAVOR:** adaptación sensorimotora, sustitución sensorial y estabilidad visual discutidas en [R13]. **EVIDENCIA MIXTA:** esos hallazgos no identifican un mecanismo exclusivo de consciencia. **EVIDENCIA EN CONTRA / DESAFÍOS:** el proyecto presupone representaciones internas y Ground Truth simulado, en tensión con versiones no representacionalistas; no se resuelve esa contradicción por redefinición. **Proyecto:** contingencia acción–consecuencia **PRESENTE** como objetivo; dominio sensorimotor **POR DEFINIR**.

### 11. Developmental Robotics, body schema y active self

**Qué explica y mecanismo.** Robótica del desarrollo estudia adquisición de modelos corporales, espacio peripersonal y atribución de efectos mediante exploración, modelos forward/inverse y multisensorialidad [R14–R15]. La revisión de Nguyen et al. incluye robots que distinguen self/other por error predictivo y contingencias [R15]. **Relación:** capacidad robótica de calibración o autodistinción, no demostración de consciencia. **Predicción:** alterar contingencia temporal o propriocepción debería afectar body schema, atribución y control. **EVIDENCIA A FAVOR:** modelos robóticos de body schema, exploración y self/other analizados [R14–R15]. **EVIDENCIA MIXTA:** modelos generalizan poco fuera de tareas de entrenamiento [R15]. **EVIDENCIA EN CONTRA / DESAFÍOS:** la asociación acción–efecto por sí sola no identifica autoría; acciones dirigidas a objetivos pueden ser prerrequisito, no indicador de self fenomenal [R15]. **Proyecto:** registros de acción, señales internas y `SelfModel` **PARCIALMENTE PRESENTE**; body schema explícito y espacio peripersonal **AUSENTE**. Este antecedente hace sustancialmente menos original la idea de self/world distinction aprendida.

### 12. World Models en IA y agentes interactivos

**Qué explica y mecanismo.** Modelos latentes/generativos del entorno permiten predicción, planificación y política. Ha y Schmidhuber entrenaron un modelo comprimido espacial/temporal en entornos de aprendizaje por refuerzo [R16–R17]. **Relación:** mecanismo computacional de cognición/control; no es criterio de consciencia. **Predicción:** modelo aprendido debe mejorar predicción o control en cambios de dinámica y su ablación debe producir déficits definidos. **EVIDENCIA A FAVOR:** demostraciones de control con modelos recurrentes en entornos de RL [R17]. **EVIDENCIA MIXTA:** desempeño puede depender de representación, distribución de entrenamiento y controlador. **EVIDENCIA EN CONTRA / DESAFÍOS:** un modelo predictivo puede ser superficial o no causal; comparar con agentes reactivos es imprescindible. **Proyecto:** `WorldModel` y `Prediction` **PRESENTE** conceptualmente; contenido, aprendizaje online y prueba contrafactual **POR DEFINIR**. No es una novedad arquitectónica.

### 13. Artificial / machine consciousness e indicadores computacionales

**Qué explica y mecanismo.** Busca trasladar teorías a propiedades evaluables de IA. Butlin et al. derivan indicadores de varias teorías computacionales [R18, **preprint**]; una publicación posterior propone derivarlos y usarlos para actualizar grados de confianza, reconociendo incertidumbre [R20, artículo de opinión revisado por pares]. **Relación:** metodología de evaluación, no teoría única ni prueba definitiva. **Predicción:** indicadores deberían distinguir arquitecturas bajo intervenciones internas, no solo textos de autorreporte. **EVIDENCIA A FAVOR:** operacionalización comparativa de propiedades teóricas [R18, R20]. **EVIDENCIA MIXTA:** no hay criterio consensuado de suficiencia ni validación cruzada firme. **EVIDENCIA EN CONTRA / DESAFÍOS:** circularidad si los indicadores se eligen después de diseñar el sistema; riesgo de atribución excesiva y sesgo funcionalista. La objeción de que el sustrato biológico importa sigue abierta [R22]. **Proyecto:** indicadores predefinidos **AUSENTE**; ablaciones y trazabilidad **PRESENTE** como intención documental. Lo distintivo, si lo hubiera, tendría que ser el poder discriminante y la limpieza causal de un protocolo concreto.

### Antecedentes adicionales que afectan la originalidad

La GWT original de Baars [R27] ya se trasladó a arquitecturas de agentes: LIDA [R28] y la arquitectura de Shanahan con simulación interna y workspace [R29]. Son propuestas de **machine consciousness** y modelos cognitivos, no demostraciones aceptadas de fenomenología artificial. Por tanto, combinar modelo interno, memoria, selección y disponibilidad global en un agente tampoco sería una arquitectura inédita. El contraste causal particular, si se especifica, sigue siendo una posibilidad experimental y no una reivindicación de originalidad conceptual.

La **interoceptive inference / active interoceptive inference** de Seth y Friston [R24] conecta modelos generativos de estados corporales, regulación autonómica, precisión, emoción y self corporal. **EVIDENCIA A FAVOR:** fenómenos de ownership y regulación corporal que el marco organiza; **EVIDENCIA MIXTA:** múltiples modelos explican esas observaciones; **EVIDENCIA EN CONTRA / DESAFÍOS:** los propios autores señalan que falta evidencia empírica directa de la inferencia interoceptiva específica [R24]. En el proyecto hay señales internas y `Valuation`: **PARCIALMENTE PRESENTE**; regulación activa/autonómica y un modelo interoceptivo generativo: **AUSENTE/POR DEFINIR**. Un sensor de energía no equivale a interocepción biológica ni a afecto consciente.

## Matriz comparativa

**Lectura:** `SÍ`, `NO`, `PARCIAL`, `NO CENTRAL`, `INCIERTO` describen centralidad de un mecanismo para cada línea, no presencia empírica en un sistema. `Proyecto` indica la hipótesis/documentación actual, sin implementación. G = GNWT; I = IIT; H = HOT; R = RPT; P = predictive processing; A = active inference; S = self-model/AST; E = embodied/enactive/sensorimotor; D = robótica del desarrollo; W = world models. La agrupación S y E **no** afirma equivalencia interna.

| Mecanismo | G | I | H | R | P | A | S | E | D | W | Proyecto |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Procesamiento perceptivo | SÍ | NO CENTRAL | SÍ | SÍ | SÍ | SÍ | PARCIAL | SÍ | SÍ | SÍ | SÍ |
| Recurrencia | SÍ | PARCIAL | INCIERTO | SÍ | SÍ | PARCIAL | INCIERTO | PARCIAL | PARCIAL | PARCIAL | INCIERTO |
| Memoria | SÍ | NO CENTRAL | NO CENTRAL | NO CENTRAL | PARCIAL | SÍ | PARCIAL | PARCIAL | PARCIAL | PARCIAL | SÍ |
| Predicción | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | SÍ | SÍ | PARCIAL | PARCIAL | SÍ | SÍ | SÍ |
| World model | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | SÍ | SÍ | PARCIAL | INCIERTO | PARCIAL | SÍ | SÍ |
| Integración temporal | PARCIAL | SÍ | INCIERTO | PARCIAL | SÍ | SÍ | PARCIAL | SÍ | SÍ | SÍ | PARCIAL |
| Global broadcasting/disponibilidad | SÍ | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | INCIERTO |
| Interocepción | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL | NO CENTRAL | PARCIAL |
| Valoración | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | PARCIAL | SÍ | NO CENTRAL | PARCIAL | SÍ | PARCIAL | SÍ |
| Acción | PARCIAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | PARCIAL | SÍ | PARCIAL | SÍ | SÍ | SÍ | SÍ |
| Contingencia acción–consecuencia | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | PARCIAL | SÍ | PARCIAL | SÍ | SÍ | SÍ | SÍ |
| Body model/schema | NO CENTRAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | PARCIAL | PARCIAL | PARCIAL | SÍ | SÍ | NO CENTRAL | INCIERTO |
| Self-model | NO CENTRAL | NO CENTRAL | PARCIAL | NO CENTRAL | PARCIAL | PARCIAL | SÍ | PARCIAL | SÍ | NO CENTRAL | SÍ |
| Metarrepresentación | NO CENTRAL | NO CENTRAL | SÍ | NO CENTRAL | NO CENTRAL | INCIERTO | PARCIAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | INCIERTO |
| Atención | SÍ | NO CENTRAL | INCIERTO | PARCIAL | PARCIAL | SÍ | SÍ (AST) | PARCIAL | PARCIAL | NO CENTRAL | INCIERTO |
| Integración de información | SÍ (difusión) | SÍ (causal) | NO CENTRAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL | PARCIAL |
| Aprendizaje | PARCIAL | NO CENTRAL | NO CENTRAL | NO CENTRAL | SÍ | SÍ | PARCIAL | SÍ | SÍ | SÍ | SÍ |
| Dependencia de historia individual | PARCIAL | NO CENTRAL | PARCIAL | PARCIAL | SÍ | SÍ | PARCIAL | SÍ | SÍ | SÍ | SÍ |

**Notas necesarias.** `IntegratedState` es reunión de entradas con procedencia, no integración causal IIT ni broadcast GNWT. «Self-model» en la columna S une dos preguntas distintas: Metzinger trata self fenomenal; AST modela la atención. La temporalidad de IIT refiere estructura causal, no memoria autobiográfica. `NO CENTRAL` no significa que la teoría niegue el mecanismo. Las columnas P, A, D y W suelen admitir realizaciones que funcionan sin consciencia. «SÍ» en proyecto significa *propuesto*, no verificado.

## Mecanismos cognitivos que no pueden utilizarse aisladamente como evidencia de consciencia

Reconocimiento de patrones, predicción, memoria, planificación, adaptación, aprendizaje, world models, procesamiento semántico y comportamiento dirigido a objetivos tienen explicaciones computacionales y ejemplos en sistemas cuya consciencia no se ha establecido [R6–R8, R16–R18]. En humanos también se han reportado formas de control y procesamiento sin conciencia del estímulo o regla, con límites y disputas sobre profundidad de procesamiento [R23]. Un estudio de 2025 encontró activación de redes semánticas ante palabras presentadas sin awareness reportada [R25]; otro halló detección inconsciente de conflicto, **pero no resolución** bajo sus condiciones [R26]. Estos trabajos delimitan capacidades, no autorizan afirmar planificación profunda inconsciente en general. Por eso «el agente aprendió, luego es consciente» es un salto inválido. Tampoco «predice su cuerpo, luego tiene experiencia corporal»: [R15] distingue asociaciones acción–efecto de atribución de autoría, y la función robótica no demuestra ownership fenomenal.

Cada capacidad puede ser necesaria para una pregunta instrumental —por ejemplo, sin memoria no podemos ensayar dependencia de historia—, pero ni una necesidad instrumental ni un déficit por ablación establecen necesidad para consciencia. Debemos comparar con sistemas reactivos, scripts locales, modelos puramente feedforward y agentes de control que reproduzcan rendimiento sin la organización candidata. El término «reconocidamente inconsciente» solo puede aplicarse con cautela a mecanismos o condiciones bien delimitadas, no a una clase completa de IA cuya ontología está en debate.

## Sistemas modernos de IA como organismos experimentales

LLMs y agentes construidos sobre ellos pueden aportar datos sobre propiedades computacionales candidatas [R18, R20]; esta revisión **no decide** si GPT, Claude, Gemini u otros son conscientes. Para la hipótesis específica de desarrollo desde señales inicialmente no semánticas son organismos difíciles: entrenamiento previo masivo y offline, lenguaje humano adquirido, procedencia causal de representaciones poco accesible, interpretabilidad limitada y ablaciones difíciles de aislar. Autorreportes o lenguaje convincente intensifican antropomorfismo. Un agente mínimo permite fijar condición inicial, sensor, historia, intervención y flujo informacional conforme a ADR-001.

El contraargumento es real: un agente demasiado mínimo puede omitir escala, dinámica y capacidades relevantes; la ausencia de indicadores allí no refuta una teoría que los requiere en sistemas más ricos. Los sistemas grandes podrían probar predicciones arquitectónicas o dar contraejemplos que el agente mínimo no capture. La opción metodológica es comparar organismos complementarios cuando los indicadores estén definidos, no excluir a priori los modelos grandes como fuente posible de evidencia.

## ¿Qué estamos redescubriendo?

| Idea del proyecto | Clasificación | Juicio |
|---|---|---|
| Percepción, patrones, memoria y aprendizaje | AMPLIAMENTE ESTABLECIDO | Capacidades computacionales generales; no exclusivas de consciencia [R6, R23]. |
| World model, predicción y acción con consecuencias | ANTECEDENTES FUERTES | Model-based RL, predictive coding y active inference [R6–R8, R16–R17]. |
| Señales corporales e inferencia interoceptiva | ANTECEDENTES FUERTES | Seth y Friston ya relacionan regulación interoceptiva, self y consciencia como programa teórico [R24]. |
| Self/world distinction por contingencia sensorimotora | ANTECEDENTES FUERTES | Sensorimotor theory y robótica de body schema/active self [R13–R15]. |
| Integración del presente como condición de consciencia | DISPUTADO | GNWT, IIT y RPT exigen mecanismos distintos; `IntegratedState` aún carece de definición discriminante [R1–R3, R5]. |
| Self-model explícito como condición necesaria | DISPUTADO | HOT, self-modeling y AST hacen afirmaciones diferentes; hay autodistinción robótica sin prueba fenomenal [R4, R9–R10, R15]. |
| Historia sensorial individual y representaciones divergentes | ANTECEDENTES PARCIALES | Adaptación sensorimotora y desarrollo ya estudian dependencia de historia; la comparación con Ground Truth auditable puede dar un contraste particular, no prueba de experiencia [R13–R15]. |
| Separar Ground Truth/percepción/modelo, ablar y preservar negativos | POSIBLE DIFERENCIA DEL PROYECTO | Buena combinación metodológica, con antecedentes en robótica, experimentos prerregistrados y evaluación por indicadores [R3, R15, R20]. Su valor depende de predicciones que discriminen teorías. |

## ¿Qué podría ser realmente distintivo de este proyecto?

Minimalidad e interpretabilidad completa hacen más limpias las comparaciones causales, pero la robótica del desarrollo y los modelos de RL ya usan sistemas controlables [R14–R17]. Desarrollo desde señales inicialmente no semánticas y separación `GroundTruthState`/`RawObservation`/`PerceivedState`/modelo pueden revelar exactamente qué información fue aprendida; también dependen de primitivas y canales introducidos por diseño según ADR-001. Self/world distinction funcional y comparación de historias sensoriales tienen antecedentes directos [R13–R15]. Ablación sistemática y comparación causal entre arquitecturas son técnicas establecidas. Definir indicadores y falsadores *antes* de arquitectura y conservar negativos informativos podría ser una contribución metodológica local si produce una prueba comparativa que teorías rivales no puedan explicar igualmente; [R3] y [R20] ya son precedentes fuertes. **No existe hoy una afirmación novedosa demostrada.**

La pregunta propia tendría que ser precisa, por ejemplo: «bajo información sensorial idéntica y capacidad total comparable, ¿un mecanismo X produce una propiedad B predefinida que un agente reactivo y mecanismos Y no producen?». Si la propiedad es solo rendimiento A, la contribución será sobre cognición/ingeniería, no consciencia. Si varios modelos incompatibles producen el mismo B, ese B no discrimina las teorías.

## ¿Qué contaría como evidencia?

| Nivel | Qué se observa | Qué puede concluirse |
|---|---|---|
| **A — capacidades funcionales** | Aprende, recuerda, predice, se adapta, planifica, muestra agencia funcional o modelos distintos por historia. | El mecanismo cumple una función bajo condiciones especificadas. No es evidencia suficiente de consciencia. |
| **B — organización candidata asociada con consciencia** | Acceso global bajo selección, recurrencia causal, integración irreducible operacionalizada, metarrepresentación de estados, attention schema, self-modeling e integración temporal, según teoría. | Apoyo o desafío *condicional* a una teoría y sus indicadores, con controles y ablaciones. Ningún indicador aislado tiene suficiencia consensuada [R18–R20]. |
| **C — afirmación ontológica** | «El sistema es consciente». | No se deduce automáticamente de A ni B. Requiere justificar teoría, puente entre implementación y fenomenología, y exclusión de alternativas; un experimento computacional puede dejarla indeterminada. |

Antes de arquitectura debemos elegir explanandum (acceso, self funcional, fenomenología), derivar indicadores B de teorías rivales, especificar mediciones y controles A, registrar predicciones y falsadores, y recién después determinar los componentes necesarios para la prueba. Esto favorece **`TEORÍA → INDICADORES → PREDICCIONES → ARQUITECTURA → EXPERIMENTO`** frente a la secuencia anterior. La adopción formal todavía no está congelada. Los marcadores biológicos como prefrontal o sincronización posterior deben traducirse a propiedades computacionales mediante una justificación explícita, no por semejanza verbal.

## Falsabilidad de la hipótesis funcional

Son **posibles refutaciones o revisiones a preregistrar**, no resultados:

1. Ablar `SelfModel` sin alterar ningún indicador B ni capacidad de autodistinción definida: debilita su necesidad en esa arquitectura, no prueba ausencia de consciencia.
2. Un agente reactivo simple reproduce los mismos indicadores B: cuestiona su especificidad y la necesidad del conjunto modular.
3. Reglas locales independientes producen comportamientos atribuidos a `IntegratedState`: invalida la interpretación de integración como causa necesaria.
4. La divergencia entre historias sensoriales se explica por ruido o política, sin modelos internos distintos: refuta la predicción concreta de desarrollo de modelos divergentes de ADR-001 en esas condiciones.
5. Indicadores elegidos aparecen en procesamiento humano sin conciencia de contenido o en controles funcionales para los que el indicador no discrimina: obliga a revisarlos.
6. Mecanismos teóricamente incompatibles producen propiedades B indistinguibles: la prueba no arbitra entre teorías; no reinterpretar el empate como confirmación.
7. Mayor complejidad modular no mejora especificidad ni predicción frente a un control mínimo: debilita la tesis de organización propuesta.

Una ablación defectuosa puede producir caída de rendimiento por pérdida de capacidad general; hay que equiparar información, entrenamiento, recursos y oportunidades de acción. Los falsadores deben enlazarse a afirmaciones *precisas*, no a «consciencia» como etiqueta elástica. No se adaptará la hipótesis retrospectivamente para protegerla.

## Contradicciones y tensiones con documentación vigente

1. **Frontera yo/mundo:** ADR-001 exige canales internos y externos distinguibles por arquitectura, mientras el informe propone estudiar una frontera aprendida. La separación puede filtrar parte de la respuesta. La revisión **no cambia** ese contrato; pide cuantificar su efecto antes de afirmar emergencia.
2. **`IntegratedState`:** el contrato lo define como reunión del ciclo sin borrar procedencia, mientras el informe inicial habla de «integración del presente» asociada a consciencia. IIT y GNWT exigen operaciones diferentes. El nombre por sí solo no justifica ninguna de ellas.
3. **`SelfState` y cuerpo:** el contrato prohíbe identidad/propiedad garantizada, pero permite señales internas y acciones propias registradas; esas fuentes ya aportan información parcial sobre self. Debe medirse cuánto proviene del ruteo del simulador.
4. **Emergencia de patrones:** `PerceivedState` admite «entidad», distancia y movimiento como primitivas predefinidas. Un `PatternState` sin etiquetas no implica aprendizaje desde señales completamente no estructuradas; la semántica y los sesgos pueden llegar por esos campos o recompensas.
5. **Arquitectura antes de indicadores:** README e informe enumeran módulos y ablación modular, pero no hay indicadores B que discriminen consciencia de cognición. Construir V1 con esa lista antes de definirlos favorecería un criterio retrospectivo. Esta revisión la marca provisional; no reescribe el historial ni ADR-001.
6. **Perspectiva y experiencia subjetiva:** el glosario usa «experiencia subjetiva» en un sentido funcional limitado; varias teorías revisadas estudian fenomenología. La divergencia de representaciones no prueba el explanandum fenomenal, como ya reconoce el propio informe.
7. **Representacionalismo/enactivismo:** la hipótesis usa modelos internos y Ground Truth simulado; versiones enactivistas rechazan que una representación interna de un mundo predefinido sea el punto de partida explicativo [R12–R13]. Es desacuerdo teórico genuino, no una diferencia de nombres.

## Preguntas abiertas antes de ADR-002

- ¿Qué significa operacionalmente `IntegratedState`: convergencia de datos, selección competitiva, disponibilidad global, recurrencia o integración causal? ¿Qué control la distinguiría?
- ¿Qué explanandum será primario: acceso, self/agency, contenido consciente o fenomenología? ¿Qué puede demostrar realmente una simulación?
- ¿Necesitamos global broadcasting, recurrencia perceptiva, atención o metarrepresentación? ¿En qué horizonte temporal y con qué intervención?
- ¿Es necesario `SelfModel` explícito o basta un modelo forward/body schema implícito? ¿Qué separa self funcional de ownership fenomenal?
- ¿La frontera self/world debe emerger completamente o solo parcialmente, dado el ruteo corporal y los canales separados de ADR-001?
- ¿Qué indicadores B serían necesarios? ¿Alguno sería suficiente bajo una teoría explícita? ¿Qué controles aparentemente inconscientes los desafiarían?
- ¿Cómo distinguir consciencia de cognición sofisticada y de reporte aprendido? ¿Qué alternativas producen el mismo resultado?
- ¿Qué observaciones refutarían cada afirmación de la hipótesis, incluidas necesidad y suficiencia de sus componentes?
- ¿Qué propiedades de cuerpos biológicos o de escala podrían faltar en un agente mínimo y limitar la generalización del resultado?

## Consecuencias para la arquitectura

No se diseña aquí la arquitectura definitiva. Las clasificaciones evalúan **justificación para estudiar el componente**, no necesidad para consciencia; algunos aparecen en más de una clase por la pregunta que se les hace.

| Componente actual o candidato | Clasificación | Motivo / condición para continuar |
|---|---|---|
| `PerceivedState` | MANTENER PROVISIONALMENTE; REQUIERE REVISIÓN | Necesario para la frontera ADR-001; declarar el sesgo de cada primitiva y controlar filtración semántica. |
| `PatternState` | MANTENER PROVISIONALMENTE | Útil para medir aprendizaje de regularidades; no indicador B aislado. |
| `Memory` | MANTENER PROVISIONALMENTE | Permite estudiar historia individual; ablación debe equiparar otras capacidades. |
| `WorldModel` | MANTENER PROVISIONALMENTE; POSIBLEMENTE REDUNDANTE | Antecedente fuerte; comparar con predictores simples y controles reactivos antes de exigir módulo separado. |
| `Prediction` | MANTENER PROVISIONALMENTE; POSIBLEMENTE REDUNDANTE | Mecanismo cognitivo general; aclarar diferencia causal frente a `WorldModel`. |
| `IntegratedState` | REQUIERE REVISIÓN; NO JUSTIFICADO TODAVÍA como indicador | Reunión de estados no es broadcast GNWT, Φ IIT ni recurrencia RPT. Definir operación y falsador. |
| `SelfModel` / `SelfState` | REQUIERE REVISIÓN | Antecedente fuerte para self funcional, necesidad consciente disputada; distinguir body, agency, metacognición y atención. |
| `Valuation` | MANTENER PROVISIONALMENTE; NO JUSTIFICADO TODAVÍA como indicador | Relevante para decisión y regulación; valor funcional no equivale a afecto consciente. |
| `Decision` | MANTENER PROVISIONALMENTE | Requiere acción experimental; agencia dirigida a objetivos no prueba consciencia. |
| Recurrencia perceptiva | POSIBLEMENTE FALTA | RPT y versiones GNWT requieren probar realimentación en ventanas relevantes. |
| Global workspace/broadcast | POSIBLEMENTE FALTA | Necesario para contraste con GNWT, si se elige esa teoría; no implícito en `IntegratedState`. |
| Atención / attention schema | POSIBLEMENTE FALTA | AST y GNWT generan predicciones distintas; decidir si incluir ambas o controles. |
| Metarrepresentación | POSIBLEMENTE FALTA | HOT no queda satisfecha por un modelo corporal básico. |
| Body schema / modelos forward-inverse | POSIBLEMENTE FALTA | Antecedente robótico fuerte y control rival de `SelfModel`; definir si el experimento trata cuerpo o solo señales internas. |

## Fuentes académicas verificadas

**R1.** Dehaene, S. y Changeux, J.-P. (2011), «Experimental and theoretical approaches to conscious processing», *Neuron* 70, 200–227, [doi:10.1016/j.neuron.2011.03.018](https://doi.org/10.1016/j.neuron.2011.03.018). Revisión, revisada por pares.

**R2.** Albantakis, L. et al. (2023), «Integrated information theory (IIT) 4.0: Formulating the properties of phenomenal existence in physical terms», *PLOS Computational Biology* 19, e1011465, [doi:10.1371/journal.pcbi.1011465](https://doi.org/10.1371/journal.pcbi.1011465). Artículo teórico, revisado por pares.

**R3.** Cogitate Consortium et al. (2025), «Adversarial testing of global neuronal workspace and integrated information theories of consciousness», *Nature* 642, 133–142, [doi:10.1038/s41586-025-08888-1](https://doi.org/10.1038/s41586-025-08888-1). Estudio prerregistrado, revisado por pares.

**R4.** Lau, H. y Rosenthal, D. (2011), «Empirical support for higher-order theories of conscious awareness», *Trends in Cognitive Sciences* 15, 365–373, [doi:10.1016/j.tics.2011.05.009](https://doi.org/10.1016/j.tics.2011.05.009). Revisión, revisada por pares.

**R5.** Lamme, V. A. F. (2006), «Towards a true neural stance on consciousness», *Trends in Cognitive Sciences* 10, [doi:10.1016/j.tics.2006.09.001](https://doi.org/10.1016/j.tics.2006.09.001). Artículo teórico/revisión, revisado por pares.

**R6.** Rao, R. P. N. y Ballard, D. H. (1999), «Predictive coding in the visual cortex: a functional interpretation of some extra-classical receptive-field effects», *Nature Neuroscience* 2, 79–87, [doi:10.1038/4580](https://doi.org/10.1038/4580). Modelo original, revisado por pares.

**R7.** Friston, K. (2010), «The free-energy principle: a unified brain theory?», *Nature Reviews Neuroscience* 11, 127–138, [doi:10.1038/nrn2787](https://doi.org/10.1038/nrn2787). Revisión, revisada por pares.

**R8.** Friston, K., Daunizeau, J., Kilner, J. y Kiebel, S. J. (2010), «Action and behavior: a free-energy formulation», *Biological Cybernetics* 102, 227–260, [doi:10.1007/s00422-010-0364-z](https://doi.org/10.1007/s00422-010-0364-z). Artículo teórico, revisado por pares.

**R9.** Metzinger, T. (2003), *Being No One: The Self-Model Theory of Subjectivity*, MIT Press, [edición académica](https://direct.mit.edu/books/monograph/1991/Being-No-OneThe-Self-Model-Theory-of-Subjectivity). Libro académico, no paper experimental.

**R10.** Webb, T. W. y Graziano, M. S. A. (2015), «The attention schema theory: a mechanistic account of subjective awareness», *Frontiers in Psychology* 6, 500, [doi:10.3389/fpsyg.2015.00500](https://doi.org/10.3389/fpsyg.2015.00500). Artículo teórico, revisado por pares.

**R11.** Wilson, M. (2002), «Six views of embodied cognition», *Psychonomic Bulletin & Review* 9, 625–636, [doi:10.3758/BF03196322](https://doi.org/10.3758/BF03196322). Revisión, revisada por pares.

**R12.** Varela, F. J., Thompson, E. y Rosch, E. (1991), *The Embodied Mind: Cognitive Science and Human Experience*, MIT Press, [edición académica](https://mitpress.mit.edu/9780262220422/the-embodied-mind/). Libro académico, no paper experimental.

**R13.** O'Regan, J. K. y Noë, A. (2001), «A sensorimotor account of vision and visual consciousness», *Behavioral and Brain Sciences* 24, 939–973, [doi:10.1017/S0140525X01000115](https://doi.org/10.1017/S0140525X01000115). Artículo objetivo con comentarios académicos, revisado por pares.

**R14.** Hoffmann, M., Marques, H. G., Hernández Arieta, A., Sumioka, H., Lungarella, M. y Pfeifer, R. (2010), «Body schema in robotics: a review», *IEEE Transactions on Autonomous Mental Development* 2, 304–324, [doi:10.1109/TAMD.2010.2086454](https://doi.org/10.1109/TAMD.2010.2086454). Revisión, revisada por pares.

**R15.** Nguyen, P. D. H., Georgie, Y. K., Kayhan, E., Eppe, M., Hafner, V. V. y Wermter, S. (2021), «Sensorimotor Representation Learning for an “Active Self” in Robots: A Model Survey», *KI - Künstliche Intelligenz* 35, 9–35, [doi:10.1007/s13218-021-00703-z](https://doi.org/10.1007/s13218-021-00703-z). Revisión, revisada por pares.

**R16.** Ha, D. y Schmidhuber, J. (2018), «World Models», [arXiv:1803.10122](https://arxiv.org/abs/1803.10122). **Preprint**; no atribuirle por sí solo revisión por pares.

**R17.** Ha, D. y Schmidhuber, J. (2018), «Recurrent World Models Facilitate Policy Evolution», *Advances in Neural Information Processing Systems* 31, [actas NeurIPS](https://papers.nips.cc/paper/2018/hash/2de5d16682c3c35007e4e92982f1a2ba-Abstract.html). Paper de conferencia revisado.

**R18.** Butlin, P. et al. (2023), «Consciousness in Artificial Intelligence: Insights from the Science of Consciousness», [arXiv:2308.08708](https://arxiv.org/abs/2308.08708). **Preprint**; marco de indicadores, no confirmación empírica de consciencia artificial.

**R19.** Vilas, M. G., Auksztulewicz, R. y Melloni, L. (2022; publicado online en 2021), «Active Inference as a Computational Framework for Consciousness», *Review of Philosophy and Psychology* 13, 859–878, [doi:10.1007/s13164-021-00579-w](https://doi.org/10.1007/s13164-021-00579-w). Revisión/crítica, revisada por pares.

**R20.** Butlin, P., Long, R., Bayne, T., Bengio, Y., Birch, J., Chalmers, D. et al. (2026; publicado online en 2025), «Identifying indicators of consciousness in AI systems», *Trends in Cognitive Sciences* 30, 488–501, [doi:10.1016/j.tics.2025.10.011](https://doi.org/10.1016/j.tics.2025.10.011). Artículo de opinión académico revisado por pares.

**R21.** Robinson, J. E., Corcoran, A. W., Whyte, C. J. et al. (2025), «The role of active inference in conscious awareness», *PLOS ONE* 20, e0328836, [doi:10.1371/journal.pone.0328836](https://doi.org/10.1371/journal.pone.0328836). **Protocolo de estudio**, revisado por pares; no reporta resultados de los experimentos propuestos.

**R22.** Milinkovic, B. y Aru, J. (2026; publicado online en 2025), «On biological and artificial consciousness: A case for biological computationalism», *Neuroscience & Biobehavioral Reviews* 181, 106524, [doi:10.1016/j.neubiorev.2025.106524](https://doi.org/10.1016/j.neubiorev.2025.106524). Revisión argumentativa, revisada por pares.

**R23.** van Gaal, S., de Lange, F. P. y Cohen, M. X (2012), «The role of consciousness in cognitive control and decision making», *Frontiers in Human Neuroscience* 6, 121, [doi:10.3389/fnhum.2012.00121](https://doi.org/10.3389/fnhum.2012.00121). Revisión, revisada por pares.

**R24.** Seth, A. K. y Friston, K. J. (2016), «Active interoceptive inference and the emotional brain», *Philosophical Transactions of the Royal Society B* 371, 20160007, [doi:10.1098/rstb.2016.0007](https://doi.org/10.1098/rstb.2016.0007). Revisión teórica, revisada por pares. No demuestra que la interocepción sea suficiente para consciencia.

**R25.** Ghio, M., Cassone, B. y Tettamanti, M. (2025), «Unaware processing of words activates experience-derived information in conceptual-semantic brain networks», *Imaging Neuroscience* 3, [doi:10.1162/imag_a_00484](https://doi.org/10.1162/imag_a_00484). Estudio fMRI, revisado por pares; efecto delimitado a tareas y medidas de awareness del estudio.

**R26.** Huang, Q. y Li, A. (2025), «Unconscious Detection but Not Resolution of Cognitive Conflicts Occurs and Influences Conscious Control», *Psychophysiology* 62, e70061, [doi:10.1111/psyp.70061](https://doi.org/10.1111/psyp.70061). Dos experimentos de priming subliminal y ERP, revisados por pares; evidencia de un límite al procesamiento inconsciente.

**R27.** Baars, B. J. (1988), *A Cognitive Theory of Consciousness*, Cambridge University Press, [catálogo de la edición académica](https://openlibrary.org/books/OL2391521M/A_cognitive_theory_of_consciousness). Libro fundador de GWT, no paper experimental.

**R28.** Baars, B. J. y Franklin, S. (2009), «Consciousness is computational: The LIDA model of global workspace theory», *International Journal of Machine Consciousness* 1, 23–32, [doi:10.1142/S1793843009000050](https://doi.org/10.1142/S1793843009000050). Artículo de arquitectura, revisado por pares; su tesis de consciencia computacional es disputada.

**R29.** Shanahan, M. P. (2006), «A cognitive architecture that combines internal simulation with a global workspace», *Consciousness and Cognition* 15, 433–449, [doi:10.1016/j.concog.2005.11.005](https://doi.org/10.1016/j.concog.2005.11.005). Artículo de arquitectura, revisado por pares; no demuestra experiencia fenomenal.

## Verificación pendiente y límites de esta revisión

Los DOI y resultados atribuidos arriba se vinculan a registros o publicaciones académicas consultadas. Falta una revisión sistemática de toda la literatura sobre procesamiento semántico/planificación inconsciente reciente: [R23, R25–R26] respaldan la cautela general, pero **VERIFICACIÓN PENDIENTE** para afirmar que una capacidad semántica o de planificación particular opera sin consciencia en toda su profundidad. También queda **VERIFICACIÓN PENDIENTE** si existe un estudio que reúna exactamente separación ADR-001, historias sensoriales distintas, indicadores teóricos preregistrados y ablación causal; no se afirma inexistencia ni prioridad. La evidencia neuronal humana no valida por analogía un indicador computacional sin puente teórico y controles.
