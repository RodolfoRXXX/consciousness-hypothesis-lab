# Percepción y estado mínimo para V1.0–V1.2

**Fecha:** 2026-09-18

**Estado:** perfil perceptivo provisional previo a código; no es un ADR.

**Alcance:** definir exactamente qué puede constituir `s_t` sin entregar identidad, semántica ni Ground Truth. Complementa la [especificación de aprendizaje y selección](v1-learning-and-action-selection.md).

## 1. Pregunta de diseño

V1.0–V1.2 necesita distinguir estímulos para aprender contingencias, pero no debe recibir la categoría que el investigador usa para generarlos. La representación mínima debe permitir:

```text
patrón sensorial externo + acción
→ consecuencia corporal sensada
```

sin convertirlo en:

```text
EntityTypeA + action_0 → etiqueta aversiva
```

La elección principal es un vector exacto de canales sensoriales externos discretos. No contiene un objeto segmentado ni una descripción semántica.

## 2. Flujo informacional obligatorio

```text
GroundTruthState
      │
      ▼
physical stimulus at sensor interface
      │
      ▼
authorized sensor transformation
      │
      ▼
ExternalRawObservation
      │
      ▼
minimal discrete readout
      │
      ▼
external_state s_t
```

No se permite una ruta `GroundTruthState → s_t`. El simulador conoce tipo, posición y reglas; el sensor solo produce lecturas locales de propiedades físicas autorizadas. La instrumentación puede correlacionar ambas vistas, pero el agente no accede a esa unión.

## 3. Microentorno V1

V1.0–V1.2 usa un **V1 micro-environment**, subconjunto experimental del mundo 2D futuro. Presenta un estímulo dentro de una relación sensorial controlada y ofrece dos acciones neutrales. No exige locomoción, giro, mapa, dirección ni distancia.

La reducción no abandona embodiment: el agente conserva cuerpo dinámico, sensores externos e internos, actuadores, consecuencias corporales e historia. Solo elimina navegación porque no es necesaria para probar aprendizaje, predicción y selección one-step.

El mundo 2D y el repertorio motor espacial permanecen en el roadmap posterior. Un resultado del microentorno no autoriza generalizar a navegación o conducta situada rica.

## 4. Canales externos mínimos

Se recomiendan **dos canales locales binarios**:

```text
ExternalRawObservation = (
    external_sensor_0,
    external_sensor_1
)

external_sensor_i ∈ {0, 1}
```

Cada canal mide la ausencia/presencia de uno de dos componentes físicos locales e independientemente configurables del estímulo, `stimulus_component_0` y `stimulus_component_1` en la descripción del simulador. El sensor devuelve `1` cuando el componente correspondiente está activo en su interfaz local y `0` cuando no lo está. No consulta el tipo verdadero. Los canales no se llaman alimento, peligro, entidad, identidad, distancia, target ni tipo. Dos canales permiten patrones distintos con componentes compartidos y recombinables; un solo canal binario solo produciría presencia/ausencia y acercaría la tarea a una etiqueta única.

Para la condición inicial, el sensor ya entrega valores discretos. Esto adopta la alternativa **C — valores sensoriales discretos generados por el sensor** y evita introducir límites de bins, tolerancias o una transformación perceptiva adicional. El alfabeto binario es estructura heredada y debe registrarse.

La regla estructural de lectura queda así fijada. El estímulo se coloca directamente en la interfaz local; el microentorno no calcula distancia ni coordenada para el agente. La condición base usa lectura determinista, sin ruido ni pérdida, disponible al comienzo del paso. Ruido, oclusión y latencias variables serán intervenciones posteriores. Debe verificarse que la implementación deriva cada bit del componente local y nunca de `EntityType`.

## 5. Patrones físicos, no labels

Tipos verdaderos diferentes deben generar patrones distinguibles a través de propiedades físicas, no mediante una tabla entregada al agente. Ejemplo estructural:

```text
estímulo X → (0, 1)
estímulo Y → (1, 1)
estímulo futuro Z → (1, 0)
```

Los valores son ejemplos de composición, no asignaciones finales a entidades. X e Y comparten un componente; Z recombina componentes existentes. La transformación debe describirse desde propiedades del estímulo y acoplamiento sensor, no como `if type == X`.

Un esquema `A → (1,0)` y `B → (0,1)` es un baseline perceptivo fuerte cercano a un one-hot categórico. No está prohibido como control, pero no es la condición principal recomendada. Incluso con patrones compartidos, si solo hay dos estímulos cada vector puede identificarlos perfectamente; por eso deben contrabalancearse asignaciones físicas entre corridas y evitar nombres semánticos.

## 6. Estado externo exacto

Para la primera implementación:

```text
s_t = external_state_t
    = (external_sensor_0_t, external_sensor_1_t)
    ∈ {0,1}²
```

La clave cognitiva es el vector completo:

```text
M[((0,1), action_0)]
```

No se crea `entity_id`, `pattern_id` persistente ni objeto segmentado. El vector no se reemplaza por `EntityTypeA` ni por un hash compartido con el motor.

Dos vectores diferentes son estados independientes:

```text
(0,1) != (1,1)
```

Aunque compartan un componente, V1.0–V1.2 no usa ese hecho. `M` indexa por igualdad del vector completo.

`(0,0)` significa que ninguno de los componentes físicos está activo. Es un estado sensorial válido, pero no forma parte de las contingencias principales X/Y; puede usarse como control de ausencia sin recibir una etiqueta especial.

## 7. Ausencia de generalización

No existe:

- distancia entre vectores;
- similitud;
- nearest neighbor;
- interpolación;
- pesos por componente;
- features consultables fuera de la clave exacta;
- transferencia de estimaciones;
- defaults dependientes de un componente.

Si `(0,1)` fue visto y `(0,0)` no, el segundo sigue `UNSEEN`. V1.4 podrá comparar exact lookup con un mecanismo que explote características compartidas usando el mismo entorno sensorial. Diseñar rasgos recombinables ahora prepara ese contraste, pero no implementa generalización.

## 8. Canales corporales fuera de `s`

La observación corporal permanece separada:

```text
BodyRawObservation = (
    body_signal_0,
    body_signal_1
)
```

Para el primer experimento, esos canales no integran la clave predictiva:

```text
s_predictive = external_state
c_t+1 = (body_signal_0_t+1, body_signal_1_t+1)
```

Así se aísla la pregunta `patrón externo + acción → consecuencia corporal anticipada` y se evita que la política sea principalmente una reacción al estado corporal actual. El protocolo debe controlar el estado corporal inicial y verificar que las señales actuales no expliquen diferencias conductuales.

Esta separación es experimental, no ontológica. ADR-001 ya separa canales internos/externos por arquitectura y esa estructura puede facilitar una frontera self/world. V1.3 probablemente necesite incorporar estado corporal actual a la predicción o selección para estudiar regulación; esa expansión requerirá un perfil nuevo.

## 9. Consecuencias corporales mínimas

Se recomiendan **dos canales corporales binarios** en la primera condición:

```text
body_signal_0 ∈ {0,1}
body_signal_1 ∈ {0,1}
```

La documentación externa interpreta el primero como funcionalmente aversivo y el segundo como funcionalmente apetitivo. Esos conceptos no aparecen en el estado del agente. Los valores binarios son un subconjunto del rango `[0,1]`; su media histórica estima frecuencia media observada y puede tomar valores intermedios.

Un solo canal aversivo sería suficiente para estudiar evitación anticipatoria con menor normatividad. Se mantienen dos porque el experimento principal ya distingue evitación y aproximación condicionadas, permite probar que la segunda dimensión solo resuelve empates en la primera y conserva comparabilidad con el alcance V1. El diseño debe incluir ablaciones de canal para medir qué evidencia adicional aporta el segundo.

Los canales no son reward ni copias de `energy`, `integrity` o sus deltas. En el microentorno, `body_signal_0 = 1` indica que el sensor corporal recibió durante la transición el evento físico discreto de perturbación asignado a ese canal; `body_signal_1 = 1`, el evento discreto de restauración asignado al suyo; ausencia del evento produce `0`. El sensor no entrega magnitud, variable corporal, delta ni rango deseable. El ruteo estable evento→canal es valencia/topografía primaria heredada y debe mantenerse separado de la identidad del estímulo.

## 10. Empate sin tolerancia

Se adopta **comparación exacta**, sin tolerancia heredada. La condición inicial usa muestras corporales binarias y contingencias controladas no conflictivas. La dimensión apetitiva se consulta cuando las medias aversivas almacenadas son exactamente iguales; por ejemplo, ambas son cero.

No se introduce tolerancia numérica, redondeo silencioso ni umbral de equivalencia. La representación numérica futura debe preservar la igualdad matemática de casos construidos como iguales. Si ruido o señales continuas vuelven infrecuente el empate exacto, eso cambia el régimen experimental y requerirá declarar discretización, tolerancia o una nueva política; no se resolverá dentro del código.

## 11. Acciones mínimas

La condición principal usa:

```text
A = {action_0, action_1}
```

Dos acciones son el mínimo para observar elección. Ambas están disponibles en cada ensayo válido del microentorno. Sus efectos físicos deben ser simétricos salvo por la contingencia experimental y deben contrabalancearse entre corridas. No se llaman acercarse, evitar, comer o interactuar dentro del estado cognitivo.

Tres o cuatro acciones espaciales agregarían navegación, orientación, oportunidades desiguales y consecuencias motoras que no son necesarias para V1.0–V1.2. Quedan para el mundo 2D posterior.

## 12. Representación candidata completa

```text
ExternalRawObservation:
    external_sensor_0 ∈ {0,1}
    external_sensor_1 ∈ {0,1}

BodyRawObservation:
    body_signal_0 ∈ {0,1}
    body_signal_1 ∈ {0,1}

ExternalDiscreteState:
    s_t = (
        external_sensor_0,
        external_sensor_1
    )

Experience:
    (
        external_state_t,
        action_t,
        external_state_t+1,
        body_consequence_t+1
    )
```

`ExternalDiscreteState` puede ser una vista mínima de `PerceivedState` o directamente una lectura discreta autorizada de `RawObservation`; no exige `PatternState`. La decisión de serialización queda para los contratos de implementación.

## 13. Qué está fijado estructuralmente y qué queda abierto

### Candidato a congelar antes de código

- microentorno sin navegación para V1.0–V1.2;
- dos canales externos locales binarios;
- valores discretos producidos por el sensor, sin binning adicional;
- `s_t` igual al vector externo completo;
- exact lookup sin IDs ni similitud;
- señales corporales fuera de la clave inicial;
- dos canales corporales binarios;
- dos acciones neutrales;
- comparación exacta, sin tolerancia;
- sensores deterministas sin ruido/pérdida y consecuencia con latencia fija de una transición;
- ambos comandos disponibles y todas las lecturas presentes en cada ensayo válido.

### Abierto antes de implementación

- magnitudes y dinámica exacta de los cambios verdaderos en `energy`/`integrity`;
- asignación y contrabalanceo de patrones X/Y entre corridas;
- temporización exacta de presentación, acción y consecuencia;
- criterio externo para invalidar una corrida si la interfaz viola las lecturas/acciones requeridas.

## 14. Auditoría adversarial

Antes de código debe intentarse refutar la neutralidad del estado:

1. ¿Cada vector funciona como ID categórico perfecto sin propiedades compartidas útiles?
2. ¿El simulador genera el canal consultando directamente `EntityType`?
3. ¿Un bit significa siempre aversivo o apetitivo por construcción?
4. ¿El orden de canales o patrones permanece ligado a una contingencia entre corridas?
5. ¿La ausencia de ruido vuelve la tarea un lookup trivial y qué afirmación permite realmente?
6. ¿La presentación controlada elimina una propiedad corporal relevante?
7. ¿Excluir señales corporales de `s` impide detectar dependencia contextual?
8. ¿El microentorno demuestra solo condicionamiento de laboratorio y no navegación?
9. ¿Una representación o logger expone el nombre X/Y al selector?
10. ¿Estados diferentes comparten defaults o inicialización que produzcan transferencia?

Un patrón perfectamente discriminable no es por sí mismo una fuga: alguna discriminabilidad es necesaria. La fuga aparece cuando la representación entrega la categoría, su consecuencia o una estructura que excede la medición física declarada.

## 15. Relación con ADR-001 y contratos

El perfil respeta ADR-001 porque toda entrada atraviesa sensores y no incluye Ground Truth ni metadata. También conserva la tensión aceptada: separar canales externos y corporales es estructura heredada.

En [data-contracts.md](../data-contracts.md), `RawObservation` admite valores de canal y separación interno/externo; eso basta. `PerceivedState` solo se necesita como vista mínima si la interfaz exige nombrar la discretización. Entidad, distancia, tamaño, movimiento, energía percibida e integridad percibida no forman parte de este perfil. `PatternState`, `SelfState` e `IntegratedState` no son necesarios.
