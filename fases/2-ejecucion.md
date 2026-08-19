# Fase 2 · Decisiones y desarrollo

Esta fase empieza cuando existe `docs/INVENTARIO.md` (de la auditoría o de la
entrevista). Tiene dos mitades, en este orden estricto: primero **las
decisiones del usuario**, después **el código**. No se escribe una línea de
`web-nueva/` con decisiones abiertas.

## Mitad A · Las decisiones (antes de programar nada)

Todo lo que se decida aquí se escribe en `docs/DECISIONES.md` con fecha y
motivo (regla 3 del AGENTS.md).

### A1 · Qué se conserva y qué no

Repasa el inventario con el usuario, en bloques pequeños. La regla por defecto
es que TODO se conserva; el objetivo de este repaso es sacar a la luz los
puntos donde él quiera cambiar algo a propósito (un texto que ya no le
representa, una página que quiere retirar, una sección nueva). Acompaña cada
punto sensible de tu recomendación razonada — qué le conviene según el
análisis de contenido y SEO que hiciste — pero decide él. Cada cambio que
apruebe va a la sección **CAMBIOS APROBADOS** del INVENTARIO.md, con su
motivo. Sin entrada ahí, en la fase 3 contará como roto.

### A2 · Las mejoras

Presenta `docs/MEJORAS.md` ordenado por lo que más gana por menos trabajo. Las
que el usuario apruebe pasan al INVENTARIO.md como puntos nuevos marcados
**[MEJORA]**, y desde ese momento son promesas: se implementan y se
verificarán en la fase 3 como todo lo demás. Las que no apruebe se quedan en
MEJORAS.md para otro día. Ninguna mejora se implementa sin pasar por aquí —
«aprovechar que estamos» sin aprobación es exactamente la clase de cambio
silencioso que este método existe para impedir.

Las mejoras marcadas **[CONTENIDO]** tienen un paso más: si el usuario las
aprueba, no se pueden implementar inventando — el material tiene que salir de
él. Para cada una, hazle las preguntas correspondientes de la Parte 1 de
`1-entrevista.md` (solo las que apliquen a esa mejora: si falta el «cómo se
trabaja conmigo», la pregunta 6; si faltan pruebas, la 3 y la 4…). Las
respuestas entran al INVENTARIO.md con su origen `[respuesta del usuario]`, y
lo que se quede sin material se marca PENDIENTE, como siempre. Así la web
nueva puede ser mejor que la vieja sin que nada se haya inventado.

### A3 · Las ampliaciones

Pregunta al usuario qué debe tener la web nueva que la vieja no tiene: páginas
nuevas, funcionalidades (una página de captación, un calendario de reservas,
un formulario distinto…), servicios que hoy no aparecen. Para cada ampliación
que pida: defínela con él (qué hace, qué URL tendrá, qué integraciones
necesita, de dónde sale su contenido — el material factual lo pone él, como
siempre) y añádela al INVENTARIO.md marcada **[AMPLIACIÓN]**. Desde ese
momento es una promesa más: se construye y se verifica en la fase 3 como todo
lo demás. Las ampliaciones también pueden llegar a mitad de desarrollo; el
circuito es el mismo — se define, se apunta, y solo entonces se construye.

### A4 · La dirección de diseño

Pregunta antes de proponer:

1. ¿Tiene referencias? Webs que le gusten (de su sector o de fuera), estilos
   que tenga en la cabeza. Si no tiene, dale dónde mirar: webs de
   competidores que admire, galerías de diseño web, las webs de las
   herramientas que usa a diario. Pídele 2 o 3 enlaces y qué le gusta de cada
   uno — le gusta «esa web» es poca información; «de esa web, lo limpio del
   menú» es una decisión.
2. ¿O ya tiene un diseño decidido y trabajado? Entonces que te diga en qué
   ficheros está, todas las plantillas siguen esa línea, y no propones
   direcciones nuevas ni «mejoras» estéticas por tu cuenta: si algo del diseño
   choca con el inventario, lo dices y decide él.

Si no hay diseño cerrado: con sus referencias, prepara **2 o 3 mockups** de la
página principal en `docs/mockups/` — HTML autocontenido que pueda abrir en su
navegador, maquetado con el contenido real del inventario, nunca con textos de
relleno — y que elija línea. La línea elegida no se queda en «el mockup 2»: se
documenta en `docs/DECISIONES.md` como sistema — colores, tipografías, y los
criterios de sus componentes — porque las demás plantillas se construirán
contra esa descripción, no reinterpretando el mockup cada vez.
Elegir un mockup y tirar es rápido; empeñarse en una idea propia muy concreta
multiplica el tiempo. Es legítimo, pero el usuario debe saber que ese coste es
una elección, no una obligación del método.

### A5 · El plan

Antes de escribir código, escribe en `docs/PLAN.md`:

- La lista de plantillas que tendrá la web (qué páginas comparten estructura).
- Un plan de trabajo por plantillas, como checklist, indicando qué puntos del
  inventario afectan a cada una.

Ese fichero es el estado vivo del desarrollo: se marca cada plantilla al
terminarla. Una sesión nueva que entre a mitad de la Mitad B debe poder saber
qué está hecho, qué está a medias y qué falta leyendo solo PLAN.md, sin
reconstruirlo desde DECISIONES.md.

## Mitad B · El desarrollo

### Las reglas del encargo

1. **Todo lo del inventario se conserva** (con la única excepción de lo que
   esté en CAMBIOS APROBADOS).
2. **Las URLs se quedan exactamente iguales**, en todos los idiomas.
3. **Los textos no se reescriben.** El diseño nuevo se monta con el contenido
   real. Si un bloque nuevo necesita un texto que no existe, no te lo
   inventes: márcalo PENDIENTE y propón el texto aparte. (Con web desde cero:
   los textos se redactan a partir del inventario y cada página se aprueba
   antes de darse por buena.)
4. **Todo se construye en `web-nueva/`.** La web en producción no se toca:
   publicar es un paso de la fase 3, aparte y con aprobación.
5. **Formularios, captación y pagos** se replican con el mismo comportamiento
   que documenta el inventario, servicio a servicio. Ninguna integración se
   elimina «porque ya no hace falta».
6. **La analítica y los píxeles** del inventario van en las mismas páginas
   donde estaban, midiendo los mismos eventos.
7. **Rendimiento y accesibilidad**: regla 7 del AGENTS.md. Una web nueva que
   carga peor que la vieja es una web rota aunque sea más bonita.
8. **Las imágenes se migran optimizándose**: toda imagen que pase de
   `web-vieja/` a `web-nueva/` se convierte a formato moderno (WebP o AVIF,
   con el peso del inventario como techo), se dimensiona según su contenedor
   y se guarda con estructura limpia (por ejemplo `assets/img/`), conservando
   el alt del inventario. Las rutas nuevas de las imágenes no rompen la regla
   de URLs: esa regla protege las páginas.

### El stack

El de la regla 5 del AGENTS.md: prácticamente estática, PHP mínimo (config,
textos compartidos, rutas, formularios), BD solo si hay una razón concreta,
sin frameworks ni compilación, lista para un hosting compartido normal.
`web-nueva/` debe quedar **autocontenida**: subir su contenido a un servidor
es todo lo que hace falta para que la web funcione.

Las **redirecciones, cabeceras de caché y forzado de HTTPS** se escriben en el
mecanismo que el servidor del inventario respeta de verdad (Parte 2b de la
auditoría): `.htaccess` si es Apache o LiteSpeed; si es nginx sin acceso a la
configuración, el panel del hosting o el PHP mínimo del stack. Una regla en un
fichero que el servidor ignora no da error — simplemente no hace nada — así
que este punto se decide con el inventario delante, no por costumbre, y se
verifica en producción en la fase 3. (Con web desde cero, el servidor se
identifica igual — cabeceras, panel, documentación del hosting — en cuanto el
usuario tenga hosting elegido, y antes de escribir estas reglas.)

### Si el origen es WordPress

La web actual es un WordPress y la nueva no lo será. Del inventario, di qué
cosas las hacía un plugin (redirecciones, schemas, formularios, caché,
sitemap) y cómo se resuelve cada una en la web nueva. Ninguna se pierde en
silencio: o se reconstruye, o el usuario aprueba explícitamente que se
descarta. Los contenidos que vivan en la base de datos (posts, páginas) se
migran a `web-nueva/` conservando sus URLs, y si vienen con shortcodes de un
page builder ([vc_row] y similares), se limpian conservando el texto y su
jerarquía. Este es el caso donde más se pierde si no hay inventario, porque
medio WordPress son plugins haciendo cosas que nadie recuerda.

### El ritmo de trabajo

Cada vez que termines una plantilla, di qué puntos del inventario le aplicaban
y cómo los has conservado, y márcala en `docs/PLAN.md`. Y mantén
`docs/DECISIONES.md` al día: cada decisión que surja por el camino (un cambio
aprobado, un texto pendiente, una duda resuelta) se apunta en el momento, no
al final.
