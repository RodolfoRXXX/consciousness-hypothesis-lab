# Contratos conceptuales de datos

**Versión:** 0.1 — 2026-09-14  
**Estado:** especificación conceptual; no define todavía clases Python ni un formato de serialización.

## Reglas transversales

`DECISIÓN DE ARQUITECTURA` Los contratos separan datos cognitivos, accesibles al agente, de instrumentación exclusiva del observador. “Accesible” significa que un módulo del agente puede leer el objeto según dependencias declaradas; no implica acceso irrestricto de todos los módulos.

- Ningún objeto cognitivo puede contener o derivar sin mediación sensorial posiciones o tipos verdaderos, causalidad real, etiquetas humanas, tick absoluto, seed, escenario, versión, commit, configuración o identidad técnica.
- Las referencias internas deben usar identificadores efímeros generados desde la observación. No deben reutilizar IDs reales del motor.
- Los nombres de campos, valores centinela, orden de colecciones y dimensiones tampoco deben codificar información prohibida.
- Una glosa humana de un patrón se almacena en metadata o análisis externo, nunca en `PatternState`.
- El agente solo conoce consecuencias reales mediante observaciones posteriores; `Outcome` es una estimación interna. El resultado objetivo permanece en `GroundTruthState` o instrumentación.
- El tick absoluto puede indexar copias externas de objetos para trazabilidad, pero ese envoltorio no entra al agente.

## Matriz de acceso

| Objeto | Productor principal | Lectores permitidos | Agente | Observador |
|---|---|---|---:|---:|
| `GroundTruthState` | motor del entorno | sensores, instrumentación | No | Sí |
| `RawObservation` | sensores | percepción, instrumentación | Sí | Sí |
| `PerceivedState` | percepción | patrones, integración, memoria, instrumentación | Sí | Sí |
| `PatternState` | aprendizaje de patrones | modelos, integración, memoria, instrumentación | Sí | Sí |
| `InternalModel` | aprendizaje/modelado | predicción, integración, decisión, instrumentación | Sí | Sí |
| `MemoryRecord` | memoria | memoria y módulos declarados | Sí | Sí |
| `Prediction` | predictor/modelo interno | valoración, decisión, aprendizaje | Sí | Sí |
| `IntegratedState` | integración | predicción, valoración, decisión, memoria | Sí | Sí |
| `SelfState` | modelado propio aprendido | integración, predicción, valoración, decisión | Sí | Sí |
| `Valuation` | valoración | decisión, memoria/aprendizaje | Sí | Sí |
| `Decision` | decisión | actuadores, memoria, instrumentación | Sí | Sí |
| `Outcome` | evaluación interna posterior | aprendizaje, memoria, valoración | Sí | Sí |
| `ExperimentMetadata` | ejecutor/instrumentación | investigador y herramientas de análisis | No | Sí |
| `ExperienceTrace` | registrador experimental | investigador; vistas cognitivas restringidas si se definen | Parcial | Sí |

## `GroundTruthState`

- **Propósito:** describir el estado operacional verdadero del mundo simulado.
- **Produce:** motor del entorno.
- **Lee:** motor, sensores e instrumentación externa.
- **Campos iniciales posibles:** cuerpos y objetos con IDs técnicos; posiciones absolutas; tipos verdaderos; propiedades físicas; recursos; daño potencial; reglas y causas de cambios; estado físico real del agente.
- **Prohibido:** acceso directo o copia de cualquiera de sus campos en entradas cognitivas. Los sensores pueden calcular señales a partir de él, pero deben aplicar su contrato de medición.

## `RawObservation`

- **Propósito:** transportar muestras sensoriales sin interpretación semántica.
- **Produce:** sensores externos e internos.
- **Lee:** módulo perceptivo, instrumentación y módulos expresamente autorizados.
- **Campos iniciales posibles:** valores de canal; modalidad; incertidumbre o calidad sensada; marca de secuencia local si surge del dispositivo; separación de canales externos/internos.
- **Prohibido:** tipo real, posición absoluta real, ID de objeto real, causalidad verdadera, etiquetas emocionales o funcionales, tick absoluto y metadata experimental. Una señal interna no puede llamarse dolor, miedo, hambre, identidad ni emoción.

## `PerceivedState`

- **Propósito:** estructurar señales como propiedades perceptivas utilizables.
- **Produce:** módulo de percepción.
- **Lee:** aprendizaje de patrones, integración, memoria e instrumentación.
- **Campos iniciales posibles:** referencia perceptiva efímera; dirección relativa; distancia, tamaño, intensidad, movimiento o cambio percibidos; energía e integridad percibidas; incertidumbre.
- **Prohibido:** amenaza, comida, enemigo, seguridad, miedo; ID o tipo verdadero; posición absoluta; certeza no sustentada por la señal. Sus primitivas deben quedar registradas como decisiones de diseño, no como emergentes.

## `PatternState`

- **Propósito:** representar activaciones o estructuras aprendidas por recurrencia entre percepción, memoria y consecuencias.
- **Produce:** módulo de aprendizaje de patrones; nombre previo permitido solo como alias histórico: `AbstractState`.
- **Lee:** modelo interno, integración, memoria e instrumentación.
- **Campos iniciales posibles:** ID interno opaco; activación; confianza; relaciones entre patrones; evidencia interna; novedad.
- **Prohibido:** etiquetas humanas predefinidas como `danger`; glosas del investigador; tipo verdadero del objeto; reglas que hagan corresponder secretamente un patrón con Ground Truth.

## `MemoryRecord`

- **Propósito:** persistir información accesible al agente sobre observaciones, estados, acciones, predicciones y consecuencias estimadas.
- **Produce:** módulo de memoria.
- **Lee:** módulos cognitivos según dependencias declaradas e instrumentación.
- **Campos iniciales posibles:** referencia de secuencia interna; fragmentos de percepción o patrones; acción registrada; predicción previa; consecuencia percibida/estimada; fuerza, incertidumbre y enlaces asociativos.
- **Prohibido:** tick absoluto, `run_id`, identidad técnica, etiquetas humanas, Ground Truth o resultado objetivo no percibido. Una referencia de secuencia no puede ser un alias del tick global.

## `InternalModel`

- **Propósito:** conservar regularidades y relaciones aprendidas que permitan interpretar y anticipar estados o consecuencias.
- **Produce:** mecanismos de aprendizaje y modelado a partir de percepciones, patrones, memoria, acciones y resultados internos.
- **Lee:** predicción, integración, decisión, aprendizaje e instrumentación.
- **Campos iniciales posibles:** variables o patrones relacionados; transición o consecuencia esperada; fuerza y confianza; incertidumbre; evidencia interna; historial de actualización autorizado.
- **Prohibido:** reglas verdaderas copiadas del motor; tipos o posiciones reales; causalidad objetiva no inferida; etiquetas humanas; tick absoluto; seed, escenario, IDs técnicos o configuración experimental.

## `Prediction`

- **Propósito:** representar estados o consecuencias esperados a partir de información interna.
- **Produce:** predictor o modelo interno.
- **Lee:** valoración, decisión, aprendizaje e instrumentación.
- **Campos iniciales posibles:** estado/patrón esperado; acción condicionante; horizonte interno; probabilidad o confianza; incertidumbre.
- **Prohibido:** futuro verdadero del simulador, seed, reglas ocultas, tick absoluto o causalidad real no aprendida.

## `IntegratedState`

- **Propósito:** reunir la información actualmente disponible para el ciclo cognitivo sin borrar su procedencia.
- **Produce:** módulo de integración.
- **Lee:** predicción, valoración, decisión, memoria e instrumentación.
- **Campos iniciales posibles:** percepciones vigentes; activaciones de patrones; contexto recuperado; predicciones; estado corporal percibido; incertidumbre y novedad.
- **Prohibido:** Ground Truth; metadata; etiquetas humanas; tick absoluto; una afirmación de “presente consciente”. La integración no es por sí sola un resultado de consciencia.

## `SelfState`

- **Propósito:** alojar regularidades aprendidas relativas al propio funcionamiento, si aparecen.
- **Produce:** módulo de modelado propio a partir de señales internas, acciones registradas, predicciones y consecuencias percibidas.
- **Lee:** integración, predicción, valoración, decisión e instrumentación.
- **Campos iniciales posibles:** estimaciones de energía/integridad; regularidades acción-cambio corporal; confianza de atribución propia/externa; expectativas de control. Los campos no tienen por qué existir desde el inicio si son objeto de aprendizaje.
- **Prohibido:** `continuity_id = agent_001`, ID técnico real, “este cuerpo soy yo”, propiedad corporal garantizada, tick absoluto o atribución causal tomada directamente del motor.

## `Valuation`

- **Propósito:** asignar relevancia funcional, costo, beneficio esperado, incertidumbre o prioridad.
- **Produce:** módulo de valoración.
- **Lee:** decisión, memoria/aprendizaje e instrumentación.
- **Campos iniciales posibles:** alternativas valoradas; componentes de costo/beneficio; relevancia; incertidumbre; novedad; confianza.
- **Prohibido:** equiparar automáticamente valores con dolor, miedo, deseo o emociones humanas; usar daño potencial verdadero no sensado; recibir etiquetas del escenario.

## `Decision`

- **Propósito:** seleccionar y registrar una acción candidata según el estado accesible.
- **Produce:** módulo de decisión.
- **Lee:** actuadores, memoria e instrumentación.
- **Campos iniciales posibles:** acción seleccionada; parámetros; alternativas internas; valoración asociada; predicción usada; confianza.
- **Prohibido:** justificaciones basadas en Ground Truth o metadata; IDs reales de objetivos; conocimiento del resultado futuro; tick absoluto.

## `Outcome`

- **Propósito:** representar dentro del agente la consecuencia percibida o estimada después de una acción o perturbación.
- **Produce:** evaluador interno a partir de observaciones nuevas, memoria de acciones y predicciones.
- **Lee:** aprendizaje, memoria, valoración e instrumentación.
- **Campos iniciales posibles:** cambios percibidos; error predictivo; variación corporal sensada; atribución incierta; confianza.
- **Prohibido:** causa verdadera entregada por el motor; delta real no sensado; etiqueta de éxito humana; afirmar autoría con certeza arquitectónica. El resultado objetivo se registra separadamente para el observador.

## `ExperimentMetadata`

- **Propósito:** reproducir, auditar y analizar una corrida desde fuera.
- **Produce:** ejecutor experimental, control de versiones e instrumentación.
- **Lee:** investigador y herramientas externas solamente.
- **Accesible al agente:** no.
- **Campos mínimos:** `run_id`; ID técnico real del agente; tick absoluto; seed; escenario; versión del software; commit Git; módulos habilitados/deshabilitados; configuración; referencias o instantáneas de Ground Truth; etiquetas humanas; posiciones absolutas y tipos verdaderos.
- **Prohibido:** cualquier flujo hacia decisión, aprendizaje, percepción, inicialización cognitiva o recompensas del agente. Si una condición experimental necesita exponer uno de estos datos, deberá hacerlo como intervención versionada mediante un canal nuevo y explícito.

## `ExperienceTrace`

- **Propósito:** conservar la secuencia auditable entre realidad, observación y estados internos.
- **Produce:** registrador experimental a partir de eventos del motor y copias de salidas de módulos.
- **Lee:** investigador y análisis externo. El agente no lee la traza completa; puede recibir una vista cognitiva que contenga únicamente datos ya autorizados.
- **Campos iniciales posibles:** referencia a `ExperimentMetadata`; tick externo; instantáneas o hashes de `GroundTruthState`; `RawObservation`; `PerceivedState`; `PatternState`; memorias modificadas; predicciones; estados integrados y propios; valoración; decisión; resultado interno; resultado objetivo; errores y procedencia.
- **Prohibido:** exponer al agente la unión de vistas o permitir que una vista cognitiva contenga tick, Ground Truth, metadata o anotaciones. La correlación externa entre niveles no debe convertirse en un canal interno.

## Validaciones documentales requeridas antes de implementar

- Definir esquema, unidades, rangos, opcionalidad y versionado de cada campo.
- Definir invariantes de no filtración y pruebas automáticas de interfaces.
- Identificar todas las primitivas de `PerceivedState` como supuestos de diseño.
- Especificar cómo se generan IDs perceptivos sin reutilizar IDs del motor.
- Separar en almacenamiento la traza del observador de cualquier memoria del agente.
- Definir latencia, ruido, alcance y pérdida de cada sensor.
