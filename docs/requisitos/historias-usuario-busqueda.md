# Historias de usuario de búsqueda

| Campo    | Valor              |
| -------- | ------------------ |
| Proyecto | Proyecto Simbiosis |
| Fecha    | 29/10/2026         |
| Versión  | 1.2                |
| Estado   | Borrador           |

## Fuentes comunes

- [Acta de UC-21 Buscar recetas](../captura/acta-acuerdos-uc-21-buscar-recetas.md), v1.1, Vigente.
- [Catálogo de requisitos](catalogo-requisitos.md), UR-08 y FR pertinentes.
- [Modelo de casos de uso](../modelos/modelo-casos-de-uso.md), UC-21.

## Épica de búsqueda

Como usuario registrado, quiero buscar recetas combinando criterios de texto, ingredientes y exclusiones, para encontrar recetas validadas que se adapten a mis preferencias alimentarias.

**Estado:** descompuesta en US-01, US-02 y US-03. Conserva la necesidad conjunta.

## Justificación de la división

La división separa tres resultados útiles independientes: especificar criterios y filtrar recetas obteniendo los resultados con su vista previa (US-01), consultar la ficha detallada de una receta seleccionada (US-02), y consultar sugerencias de recetas o correcciones ante búsquedas sin coincidencias (US-03). Cada historia aporta valor por sí sola y puede desarrollarse de forma independiente.

## US-01

**Título:** Especificar criterios y filtrar recetas
Como usuario registrado, quiero indicar ingredientes a incluir, ingredientes a excluir y una palabra o frase clave para filtrar recetas publicadas y validadas, para encontrar recetas que cumplan mis preferencias alimentarias sin tener que revisar el catálogo completo.
**Fuentes:** UR-08; UC-21; FR-085, FR-086, FR-087; acta, §2.1 (Criterios de búsqueda).

### Criterios de aceptación

- **CA-01.** Dado que el usuario tiene sesión iniciada y accede al formulario de búsqueda, cuando indica al menos un ingrediente a incluir y solicita buscar, entonces el sistema muestra únicamente recetas publicadas y validadas que contengan todos los ingredientes indicados.
- **CA-02.** Dado que el usuario ha indicado ingredientes a incluir y a excluir sin conflictos entre ellos, cuando solicita buscar, entonces el sistema muestra únicamente recetas que contienen todos los ingredientes incluidos y ninguno de los excluidos.
- **CA-03.** Dado que el usuario indica el mismo ingrediente tanto para incluirlo como para excluirlo, cuando solicita buscar, entonces el sistema señala el conflicto y no ejecuta la búsqueda hasta que el usuario lo corrija.

## US-02

**Título:** Consultar el detalle de una receta

Como usuario registrado, quiero consultar la ficha detallada de una receta seleccionada, para conocer sus ingredientes, instrucciones de preparación e información de validación antes de decidir elaborarla.

**Fuentes:** UR-08; UC-21; FR-056, FR-066, FR-192; acta, §2.2 (Resultados y detalle).

### Criterios de aceptación

- **CA-01.** Dado que el usuario selecciona una receta para consultar su contenido completo, cuando el sistema presenta la ficha detallada, entonces muestra título, imagen si existe, lista de ingredientes, instrucciones de preparación, tiempo de cocción, número de porciones, alias de quien la publicó e insignia de validación.
- **CA-02.** Dado que la receta seleccionada no dispone de imagen asociada, cuando se presenta la ficha detallada, entonces el sistema muestra la indicación «Sin imagen» sin omitir ninguno de los restantes datos obligatorios.
- **CA-03.** Dado que el usuario finaliza la consulta del detalle de una receta, cuando solicita volver a la vista anterior, entonces el sistema retorna al listado conservando los criterios y el orden de la búsqueda previa.

## US-03

**Título:** Consultar sugerencias y correcciones de búsqueda

Como usuario registrado, quiero consultar sugerencias de recetas y correcciones ortográficas ante una búsqueda sin resultados, para encontrar recetas afines ajustando mis criterios de búsqueda.

**Fuentes:** UR-08; UC-21; FR-102; acta, §2.3 (Búsqueda sin resultados).

### Criterios de aceptación

- **CA-01.** Dado que una búsqueda realizada no arroja coincidencias y el texto introducido admite corrección ortográfica o existen recetas alternativas, cuando el sistema presenta la respuesta, entonces muestra las sugerencias propuestas diferenciadas del área de resultados sin ejecutarlas automáticamente.
- **CA-02.** Dado que la búsqueda inicial contenía ingredientes excluidos, cuando el sistema genera sugerencias o recetas alternativas, entonces ninguna propuesta incluye ingredientes que hubieran sido marcados como exclusión.
- **CA-03.** Dado que el usuario decide aplicar una de las sugerencias o correcciones propuestas, cuando la selecciona, entonces el sistema traslada los nuevos criterios al formulario de búsqueda sin ejecutarla automáticamente, permitiendo al usuario revisarlos y confirmar la consulta.

## Revisión INVEST

La revisión abarca US-01, US-02 y US-03. «Aplicado» indica si se ha realizado la comprobación. «Cumple» indica si todas las historias cumplen el criterio. Si alguna no lo cumple, indicar «No» e identificar la historia y el motivo en la justificación. Si no se ha realizado la comprobación o faltan datos, indicar «Pendiente» en «Cumple».

| Criterio      | Pregunta de revisión                                                                                                                                              | Aplicado | Cumple | Justificación                                                                                                                                                                                                                                                                                                                      |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Independiente | ¿Puede implementarse cada historia y ofrecer un resultado útil sin implementar antes las otras historias del conjunto? Puede compartir infraestructura con ellas. | Sí       | Sí     | Cada historia ofrece valor de forma autónoma: US-01 permite filtrar y listar; US-02 implementa la vista de detalle para cualquier receta accesible sin requerir el motor de filtros; US-03 proporciona el mecanismo de sugerencias y correcciones ante búsquedas sin coincidencias sin acoplarse al manejo de errores del sistema. |
| Negociable    | ¿Cada historia explica qué necesita la persona y deja margen para discutir los detalles de la solución, respetando los acuerdos confirmados?                      | Sí       | Sí     | Describen capacidades y beneficios sin imponer detalles tecnológicos ni decisiones cerradas de diseño de interfaz, respetando los acuerdos confirmados del acta.                                                                                                                                                                   |
| Valiosa       | ¿La parte «para…» de cada historia explica el beneficio que obtiene la persona al usar esa capacidad?                                                             | Sí       | Sí     | Cada historia define claramente el beneficio: US-01 encontrar recetas adecuadas sin revisar todo el catálogo; US-02 conocer la información completa antes de cocinar; US-03 obtener alternativas afines sin necesidad de redefinir manualmente todos los criterios.                                                                |
| Estimable     | ¿Están claros el alcance y los datos necesarios para estimar el trabajo de cada historia?                                                                         | Sí       | Sí     | El alcance de cada historia está claramente delimitado por sus criterios de aceptación y las reglas de negocio del acta (campos de vista previa, detalle y lógica de sugerencias sin exclusiones), evitando mezclas con fallos de carga o errores de servidor.                                                                     |
| Pequeña       | ¿Se centra cada historia en una única capacidad de alcance manejable?                                                                                             | Sí       | Sí     | Cada historia aborda una capacidad atómica: US-01 filtrar y listar resultados; US-02 consultar la ficha de detalle; US-03 consultar sugerencias y correcciones ortográficas. No se mezclan capacidades en ninguna historia.                                                                                                        |
| Comprobable   | ¿Los criterios de aceptación de cada historia describen acciones y resultados observables que permiten distinguir un comportamiento correcto de uno incorrecto?   | Sí       | Sí     | Todos los criterios de aceptación siguen la estructura Dado-Cuando-Entonces y especifican resultados verificables y observables de manera unívoca.                                                                                                                                                                                 |

## Dudas pendientes

Ninguna.
