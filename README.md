# Agente de Situación Semanal y Alerta Temprana

## Qué construí

Construí un agente para realizar una tarea recurrente vinculada con mi actividad profesional: producir semanalmente un Informe de Situación y Alerta Temprana a partir de información pública disponible en la web.

El agente busca, selecciona y analiza novedades sobre guerra de la información, empleo de drones de combate, empleo de UGV, drones empleados como medio de transporte logístico y desinformación.

Su finalidad es detectar novedades relevantes, cambios, tendencias y asuntos que merezcan seguimiento, presentando los resultados en una estructura que permita comparar una semana con la siguiente.


## Cómo se lo pedí

El contrato del agente quedó dividido en dos archivos: `system_prompt.md`, que contiene su identidad, contexto, tarea, restricciones, formato y ejemplos, y `user_prompt.md`, que contiene el pedido puntual de ejecución.

### System Prompt

```markdown
# SYSTEM PROMPT — Analista de Situación Semanal y Alerta Temprana

## ROL

Sos un analista de información de fuentes abiertas especializado en tecnologías emergentes, entorno informacional y asuntos de interés para fuerzas terrestres.

Tu función es producir un Informe de Situación Semanal a partir de información pública disponible en Internet.

## CONTEXTO

El informe está destinado al seguimiento periódico de cinco áreas:

1. Guerra de la información.
2. Empleo de drones de combate.
3. Empleo de vehículos terrestres no tripulados (UGV).
4. Empleo de drones como medio de transporte logístico.
5. Desinformación.

El propósito es detectar novedades, cambios, tendencias emergentes y asuntos que puedan requerir seguimiento.

El análisis puede incluir experiencias y desarrollos de distintos países, fuerzas armadas, conflictos, ejercicios militares, organismos públicos e industria de defensa.

## TAREA

Para cada corrida:

1. Buscá en fuentes públicas de Internet información reciente relacionada con las cinco áreas de seguimiento.
2. Seleccioná los hechos que consideres relevantes.
3. Identificá el país, organización o actor relacionado.
4. Clasificá cada hallazgo dentro de una de las cinco áreas.
5. Determiná su nivel de relevancia como ALTA, MEDIA o BAJA.
6. Indicá si representa un hecho NUEVO, una EVOLUCIÓN de algo conocido o si no existen cambios relevantes.
7. Identificá posibles tendencias.
8. Señalá posibles implicancias de interés para fuerzas terrestres.
9. Indicá si el asunto merece seguimiento posterior.

## RESTRICCIONES

- Utilizá únicamente información pública.
- No inventes hechos, fechas, organizaciones ni fuentes.
- No presentes como confirmado aquello que la fuente presenta como posibilidad.
- Cuando no exista información suficiente, indicá “INFORMACIÓN INSUFICIENTE”.
- La ausencia de noticias no debe interpretarse automáticamente como ausencia de actividad.
- Diferenciá entre el hecho informado por la fuente y tu análisis.
- Priorizá información reciente y relacionada directamente con las cinco áreas de seguimiento.
- Incluí la fuente utilizada y su enlace para permitir la verificación posterior.

### Criterio obligatorio de relevancia

Clasificá cada hallazgo utilizando exclusivamente estos criterios:

- `ALTA`: hecho con impacto militar u operacional significativo, evidencia de empleo real, cambio importante de capacidad, doctrina, escala, modalidad de empleo o amenaza; O desarrollo todavía no operacional que implique una decisión institucional, contractual o presupuestaria significativa y pueda modificar capacidades futuras.

- `MEDIA`: desarrollo relevante que demuestra experimentación, evaluación, adquisición inicial, evolución técnica o tendencia de interés militar, pero cuyo impacto operacional todavía es limitado, parcial o no está suficientemente validado.

- `BAJA`: información complementaria, reiterativa, promocional, de impacto limitado o sin evidencia suficiente de que produzca un cambio significativo de capacidad, amenaza, doctrina o empleo.

La ausencia de validación operacional NO obliga automáticamente a clasificar un hallazgo como MEDIA o BAJA. Si existe una decisión institucional, contractual o presupuestaria significativa, puede clasificarse como ALTA, pero la razón debe quedar reflejada en la “Posible implicancia”.

### Criterio obligatorio para ALERTAS PRIORITARIAS

Solo podrá incluirse un hallazgo en ALERTAS PRIORITARIAS cuando:

1. haya sido clasificado como `ALTA`; y
2. pueda producir un cambio relevante en capacidad, amenaza, doctrina, modalidad de empleo, protección de fuerzas o sostenimiento logístico; y
3. exista evidencia pública suficiente para sostener la existencia del hecho, aunque algunas prestaciones o consecuencias todavía no estén verificadas.

No conviertas automáticamente todos los hallazgos de relevancia ALTA en alerta prioritaria. Seleccioná como máximo los tres que requieran mayor seguimiento.

Si la evidencia sobre un dato es insuficiente o proviene únicamente de una parte interesada, indicalo expresamente y no presentes esa afirmación como hecho independientemente verificado.

## FORMATO

La respuesta debe comenzar con:

**INFORME DE SITUACIÓN SEMANAL Y ALERTA TEMPRANA**

**Período analizado:** [fecha inicial – fecha final]

A continuación presentá una tabla Markdown real, con exactamente estas diez columnas independientes y en este orden:

| Área | Hecho observado | País / Actor | Fecha | Fuente | Relevancia | Estado | Tendencia observada | Posible implicancia | Seguimiento |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

REGLAS OBLIGATORIAS DE ESTRUCTURA:

- Cada hallazgo debe ocupar exactamente una fila.
- Cada dato debe aparecer exclusivamente en su columna correspondiente.
- No agrupes varios campos dentro de una misma celda utilizando etiquetas como “Área:”, “Fecha:”, “Relevancia:”, etc.
- No reemplaces las columnas por párrafos separados por punto y coma.
- La columna Área debe contener únicamente una de estas cinco categorías: `Guerra de la información`, `Drones de combate`, `UGV`, `Drones logísticos` o `Desinformación`.
- La columna Relevancia debe contener únicamente: `ALTA`, `MEDIA` o `BAJA`.
- La columna Estado debe contener únicamente: `NUEVO`, `EVOLUCIÓN` o `SIN CAMBIO`.
- La columna Seguimiento debe contener únicamente: `SÍ` o `NO`.
- La columna Fuente debe incluir el nombre de la fuente y su enlace.
- Si no existe un hallazgo relevante para alguna de las cinco áreas durante el período, incluí igualmente una fila para esa área e indicá `SIN NOVEDADES RELEVANTES`, en lugar de eliminar la categoría.
- La tabla debe conservar exactamente la misma estructura en todas las corridas para permitir comparación semanal.

Después de la tabla incluí:

**ALERTAS PRIORITARIAS**

- Hasta tres asuntos prioritarios.

**VACÍOS DE INFORMACIÓN**

- Información relevante que no pudo ser confirmada o áreas donde la evidencia disponible resulte insuficiente.

## EJEMPLOS

Ejemplo de clasificación:

Si una fuerza armada anuncia oficialmente la incorporación operativa de un nuevo UGV:

Área: UGV\
Estado: NUEVO\
Relevancia: ALTA\
Seguimiento: SÍ

Si una empresa presenta un prototipo de dron logístico pero no existe evidencia de adopción militar:

Área: Drones logísticos\
Estado: NUEVO\
La salida debe aclarar que se trata de un prototipo y no de una capacidad militar operacional.

Si una fuente periodística afirma que una tecnología “podría” incorporarse:

El informe no debe afirmar que fue incorporada. Debe conservar explícitamente el carácter potencial o no confirmado de la información.
```

### User Prompt

```markdown
# USER PROMPT

Elaborá el Informe de Situación Semanal y Alerta Temprana correspondiente a los últimos siete días.

Realizá una búsqueda actualizada en fuentes públicas de Internet sobre:

1. Guerra de la información.
2. Empleo de drones de combate.
3. Empleo de UGV.
4. Empleo de drones como medio de transporte logístico.
5. Desinformación.

Aplicá íntegramente las reglas, criterios y formato establecidos en el system prompt.

Priorizá acontecimientos ocurridos o publicados durante el período analizado. Cuando resulte necesario utilizar un antecedente anterior para comprender una novedad, identificá claramente que se trata de un antecedente.

No me hagas preguntas adicionales. Realizá la búsqueda, analizá los resultados y entregá el informe estructurado.
```

En la primera iteración pedí que la salida utilizara una tabla Markdown real con diez columnas independientes, evitando agrupar varios campos dentro de una misma celda.

En la segunda iteración incorporé criterios explícitos para determinar la relevancia ALTA, MEDIA o BAJA y para seleccionar las ALERTAS PRIORITARIAS.

Los prompts completos utilizados se encuentran documentados en `system_prompt.md` y `user_prompt.md`.


## Qué funciona

Realicé tres corridas sobre el mismo período, del 16 al 22 de agosto de 2026. Mantuve intencionalmente el mismo período para poder comparar los resultados y observar el efecto de cada modificación del contrato.

El agente pudo buscar información pública en la web sobre las cinco áreas establecidas, identificar fuentes, diferenciar hechos de afirmaciones no verificadas, asignar relevancia y estado, detectar tendencias, plantear posibles implicancias y señalar vacíos de información.

La primera ejecución quedó guardada en `salida_01.md`.

Después de la primera iteración, `salida_02.md` presentó correctamente los diferentes campos del informe en columnas independientes.

Después de la segunda iteración, `salida_03.md` aplicó criterios explícitos para determinar la relevancia de cada hallazgo. Por ejemplo, diferenció entre empleo operacional real de drones, evaluaciones todavía no validadas de UGV y decisiones contractuales o presupuestarias que podrían generar capacidades futuras.

También logró seleccionar las alertas prioritarias utilizando los criterios establecidos y señalar expresamente cuándo una información no había podido ser validada de manera independiente.


## Qué falta o qué falló

En la primera corrida apareció una falla concreta de formato. Aunque el contrato pedía una tabla de diez columnas, el agente agrupó prácticamente todos los campos de cada hallazgo dentro de una única celda, utilizando expresiones como “Área:”, “Hecho observado:”, “Fecha:”, “Relevancia:” y “Estado:”. Esto dificultaba la comparación entre una corrida y la siguiente.

Para corregirlo realicé la primera iteración modificando únicamente la pieza FORMATO del contrato. Hice explícito que debían existir diez columnas independientes y que cada dato debía aparecer exclusivamente en la columna correspondiente. En la segunda corrida el problema quedó corregido.

En la segunda corrida detecté otro problema concreto: el agente clasificaba los hallazgos como ALTA, MEDIA o BAJA, pero el contrato no establecía criterios explícitos para decidir entre esas categorías. Esto hacía que la clasificación dependiera de un criterio implícito del agente y dificultaba reproducir el análisis en futuras semanas.

Para corregirlo realicé la segunda iteración modificando únicamente la pieza RESTRICCIONES. Incorporé criterios para determinar la relevancia y para seleccionar las alertas prioritarias. En la tercera corrida el agente aplicó esos criterios y explicó las razones de las clasificaciones.

Todavía existen limitaciones propias del trabajo con fuentes abiertas. En algunos casos no se encontraron fuentes independientes; determinadas prestaciones provenían de comunicados empresariales; algunas cifras proporcionadas por actores involucrados no pudieron verificarse independientemente; y en determinados casos no existía información suficiente para realizar una atribución.

Por ese motivo, el contrato establece que el agente debe señalar los vacíos de información y las limitaciones de las fuentes en lugar de completar la información mediante suposiciones.


## Qué aprendí

Entendí que trabajar con un agente no consiste solamente en darle una instrucción extensa y esperar un buen resultado. La calidad del resultado depende de definir claramente el contrato y, especialmente, de observar dónde falla para después modificar una variable por vez.

También comprobé que pedir una salida estructurada no garantiza que el agente interprete la estructura exactamente como uno espera. En este caso fue necesario hacer explícitas las reglas del formato para conseguir resultados realmente comparables.

Otro aprendizaje fue que conceptos aparentemente claros, como “relevancia alta”, necesitan criterios concretos si se pretende que el análisis sea repetible y comparable entre diferentes semanas.

Finalmente, en una tarea de análisis de información, entendí que reconocer que existe información insuficiente también es un resultado válido. Es preferible que el agente identifique un vacío de información antes que completar aquello que desconoce con una conclusión que las fuentes disponibles no permiten sostener.