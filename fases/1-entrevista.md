# Fase 1 (variante) · Entrevista: el inventario cuando no hay web que auditar

Esta variante sustituye a `1-auditoria.md` cuando **no existe web anterior**
(marca nueva, primer proyecto). Las fases 2 y 3 funcionan igual después.

La diferencia de fondo: en un rediseño el peligro es **perder** lo que ya
funciona, y por eso se audita. Desde cero no hay nada que perder — el peligro
es que la IA **se lo invente**. El copy, la estrategia de venta, las
descripciones de servicios no se pueden copiar de ningún sitio, y una IA
rellena esos huecos con texto verosímil sin avisar. Así que aquí el inventario
no sale de auditar un código: sale de entrevistar al usuario. El documento
resultante se llama igual, `docs/INVENTARIO.md`, para que el resto del método
no cambie. (`web-vieja/` se queda vacía: no hay web vieja.)

La regla más importante (regla 2 del AGENTS.md, que aquí es la protagonista):
**nada factual se inventa**. Los datos del negocio, los precios, las cifras,
los testimonios, los nombres de clientes salen de las respuestas del usuario o
no existen. El agente redacta y ordena; el material lo pone el usuario. Un
hueco sin material se queda marcado como PENDIENTE.

## Parte 1 · La entrevista

Haz las preguntas de una en una o en bloques pequeños, y no pases al siguiente
bloque hasta tener respuestas concretas:

1. **Qué vendo.** Cada servicio o producto, con sus precios si los da. Qué se
   puede comprar directamente y qué empieza por un contacto.
2. **A quién.** Quién es el cliente que quiere, cómo describe ese cliente su
   problema (con sus palabras, no con las del negocio), y quién NO es su
   cliente.
3. **Por qué él.** Qué le diferencia de verdad, con pruebas: años, casos,
   cifras que pueda enseñar. Si no hay pruebas de algo, no se afirma.
4. **Material real.** Qué existe ya: testimonios reales (con permiso), logos
   de clientes, fotos, casos. Lo que no exista no aparece en la web, ni
   siquiera «de ejemplo»: nada de bloques de testimonios de relleno esperando
   a que algún día haya testimonios.
5. **Qué tiene que pasar.** La acción que quiere que haga el visitante en cada
   página (llamar, pagar, escribir, suscribirse), por orden de importancia.
6. **Cómo se trabaja con él.** Qué pasa cuando alguien contrata: el proceso,
   los plazos, qué incluye y qué no. Y las dos o tres objeciones que más se
   repiten, con la respuesta real que da. Esto es media página de servicio.
7. **Dónde.** Si el negocio es local o trabaja por zonas: dirección, áreas de
   servicio. Condiciona la estructura de URLs y el schema de la Parte 2.

## Parte 2 · Decidir lo que en un rediseño ya vendría dado

Aquí el agente propone y el usuario aprueba. Acompaña cada propuesta de su
porqué.

8. **Estructura de URLs.** La estructura completa de páginas y URLs, con la
   intención de búsqueda de cada una si el SEO importa. Este es el momento en
   que decidirlo es gratis: cambiarlo con la web publicada ya no lo es.
9. **Idiomas.** Si habrá más de uno, el esquema de URLs por idioma desde el
   día uno.
10. **Titles, descriptions y H1.** La tabla completa: URL → title → meta
    description → h1, derivados de la intención de búsqueda de cada página.
11. **Datos estructurados.** Qué schema corresponde a cada plantilla (negocio
    local, servicio, FAQ, lo que aplique) y con qué datos se rellenará.
12. **Enlazado interno.** El plan de qué página enlaza a cuál y desde dónde
    (menú, contenido, footer), pensado para la estructura del punto 8.
13. **Lo técnico mínimo.** Sitemap, robots.txt, canonicals, página 404, y la
    convención de nombres de fichero y alt de las imágenes.
14. **Integraciones.** Qué hace falta montar y con qué servicio: formulario (a
    dónde envía), captación de correos, pagos si los hay, analítica, cookies y
    textos legales. De cada sitio donde se recojan datos personales, deja
    apuntado quién es el responsable, para qué se recogen y a qué servicio van
    a parar: la fase 2 construye con eso el consentimiento y la información de
    primera capa de cada formulario («Lo legal, de serie»), y los textos los
    aprueba el usuario.

## Formato de salida

`docs/INVENTARIO.md` con las dos partes. Los puntos 8 a 13 son la base mínima
de SEO de la web: no sustituyen a un trabajo de SEO de verdad, pero evitan lo
contrario, que es una web bonita sin base sobre la que luego no se puede
trabajar. Cada afirmación de la Parte 1 lleva su origen: `[respuesta del
usuario]` o `[PENDIENTE]`. La Parte 2 queda como especificación comprobable:
en la fase 3 se verificará la web contra este documento, punto por punto, así
que nada de generalidades.

## Nota para la fase 2 con web desde cero

En la fase 2, la regla «los textos no se reescriben» se lee así: los textos
los redacta el agente **a partir del inventario**, y cada página se aprueba
con el usuario antes de darse por buena. Lo factual que no esté en el
inventario no puede aparecer. Y en la fase 3 se comprobará además que ningún
PENDIENTE se rellenó solo por el camino — que es la forma silenciosa en que la
IA inventa.
