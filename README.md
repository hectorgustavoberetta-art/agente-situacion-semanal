# Agente de Situación Semanal y Alerta Temprana

## Qué construí

Construí un agente para realizar una tarea recurrente vinculada con mi actividad profesional: producir semanalmente un Informe de Situación y Alerta Temprana a partir de información pública disponible en la web.

El agente busca, selecciona y analiza novedades sobre guerra de la información, empleo de drones de combate, empleo de UGV, drones empleados como medio de transporte logístico y desinformación.

Su finalidad es detectar novedades relevantes, cambios, tendencias y asuntos que merezcan seguimiento, presentando los resultados en una estructura que permita comparar una semana con la siguiente.


## Cómo se lo pedí

El contrato del agente quedó dividido en dos archivos: `system_prompt.md`, que contiene su identidad, contexto, tarea, restricciones, formato y ejemplos, y `user_prompt.md`, que contiene el pedido puntual de ejecución.

Las principales instrucciones utilizadas fueron:

1. “Actuá como un analista de información especializado en seguimiento de fuentes abiertas y elaboración de informes de situación para apoyar el análisis de tendencias vinculadas con fuerzas terrestres.”

2. “Una vez por semana, buscá información pública disponible en la web correspondiente a los últimos siete días sobre: guerra de la información, empleo de drones de combate, empleo de UGV, empleo de drones como medio de transporte logístico y desinformación.”

3. “Identificá novedades relevantes, cambios, tendencias y asuntos que merezcan seguimiento.”

4. “La salida debe ser estructurada y mantener el mismo formato entre corridas para permitir la comparación semanal.”

5. En la primera iteración pedí que la salida utilizara una tabla Markdown real con diez columnas independientes, evitando agrupar varios campos dentro de una misma celda.

6. En la segunda iteración incorporé criterios explícitos para determinar la relevancia ALTA, MEDIA o BAJA y para seleccionar las ALERTAS PRIORITARIAS.

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