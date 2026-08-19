# Fase 1 · Auditoría de la web actual

Esta fase se usa cuando **existe una web que va a ser sustituida**. Si no hay
web previa (marca nueva, primer proyecto), esta fase se sustituye por
`1-entrevista.md` y las fases 2 y 3 funcionan igual.

El resultado de esta fase son dos ficheros:

- `docs/INVENTARIO.md` — lo que no se puede perder, punto por punto y
  comprobable. Será el contrato de la fase 2 y la lista de verificación de la 3.
- `docs/MEJORAS.md` — las carencias detectadas por el camino, como lista de
  oportunidades que el usuario decidirá en la fase 2.

**Durante toda esta fase: solo lectura. No se cambia nada de la web actual.**

## Paso 0 · Onboarding: lo que el agente necesita del usuario

Antes de auditar nada, repasa esta lista con el usuario, punto por punto, y no
sigas hasta tenerla cerrada. Y «auditar nada» incluye la web publicada: aunque
ya tengas la URL, no adelantes una revisión externa (descargar el HTML
público, recorrer URLs, analizar cabeceras) mientras esperas los accesos. La
auditoría se hace una sola vez, con el código y la web en vivo delante a la
vez; empezar por la mitad externa produce un inventario a medias que luego hay
que rehacer y mezclar. Solo si el usuario no puede dar ningún acceso al código
se audita únicamente lo público — dejándolo apuntado como límite en el
inventario.

1. **Copia de seguridad.** Confirma que existe una copia completa de ficheros
   y base de datos, hecha hoy. Si no existe, guíale para hacerla antes de
   continuar. No es negociable.
2. **Acceso al código.** Auditar solo el HTML público deja fuera las
   redirecciones, la configuración del servidor y todo lo que hace el código
   por detrás. Ofrécele las opciones por orden de sencillez y ayúdale con la
   que elija:
   - **FTP**: crear en su hosting una cuenta FTP (idealmente limitada a la
     carpeta de la web) y darle las credenciales al agente.
   - **SSH o repositorio Git**, si los tiene y sabe usarlos.
   - **Copia manual**: descargarse el código él mismo y soltarlo en
     `web-vieja/`.
3. **La base de datos**, si la web la usa (WordPress la usa siempre): un
   export SQL, o al menos el XML de exportación de WordPress (Herramientas →
   Exportar) junto al sitemap. Si la BD contiene datos personales de terceros
   (clientes, pedidos), recomiéndale exportar filtrando esas tablas.
4. **Credenciales a `.secrets/`.** Todo lo que te dé (FTP, BD) se guarda en
   ficheros dentro de `.secrets/`, nunca en otro sitio. Recuérdale que no las
   pegue en ficheros del proyecto.
5. **Descarga.** Con el acceso resuelto, descarga el código completo (y el
   export de BD) a `web-vieja/`. A partir de aquí trabajas sobre esa copia.
6. **El hosting.** Pregúntale qué hosting tiene y desde qué panel lo gestiona
   (cPanel, Plesk, panel propio). No le preguntes más que eso: qué servidor
   corre por debajo no tiene por qué saberlo él — lo averiguas tú en la
   Parte 2b con esas pistas.
7. **Encaje del kit.** Comprueba lo de «Para quién NO es este kit» del
   AGENTS.md y, si aplica, dilo ahora.

## Parte 1 · SEO: lo que sostiene las visitas

Cada punto tiene que ser comprobable: nada de generalidades, cita URLs,
ficheros y valores concretos tal como están hoy.

1. **URLs.** Lista todas las URLs de la web (sitemap, enlaces internos, y las
   que encuentres en el código). Esta lista es sagrada: en el rediseño se
   conservan todas. Si alguna no se pudiera conservar, necesitará una
   redirección 301.
2. **Redirecciones existentes.** Busca redirecciones ya configuradas
   (.htaccess, configuración del servidor, código), y anota en qué mecanismo
   vive cada una (ver Parte 2b). Se pierden en casi todos los rediseños y
   nadie se entera hasta meses después.
3. **Idiomas.** Si la web tiene más de un idioma: qué URLs tiene cada versión,
   cómo están enlazadas entre sí y si hay etiquetas hreflang. Documenta el
   esquema exacto.
4. **Enlazado interno.** Qué páginas enlazan a cuáles (menú, footer, enlaces
   dentro del contenido). El enlazado cambia solo al cambiar la plantilla, así
   que hay que saber cuál era.
5. **Datos estructurados.** Todos los schemas (JSON-LD, microdata) de cada
   plantilla, con su contenido.
6. **Titles, descriptions y H1.** Tabla completa: URL → title → meta
   description → h1.
7. **El texto que posiciona.** Para cada página que reciba tráfico orgánico,
   guarda el contenido de texto tal cual. Al remaquetar se tiende a reescribir,
   y con el texto se va lo que traía visitas. Si no sabes qué páginas reciben
   tráfico, márcalas todas como «conservar texto salvo aprobación explícita».
8. **Canonicals, robots.txt y sitemap.** Contenido actual de los tres. Y las
   metas robots página a página: si algo está hoy en noindex o nofollow, es
   una decisión que hay que conservar, no un descuido que perder.
9. **Imágenes.** Nombres de fichero y atributos alt de las imágenes de
   contenido, y cómo se sirven: peso aproximado, formato, srcset,
   lazy-loading, CDN si lo hay. Si hoy están optimizadas, la web nueva no
   puede servirlas peor.
10. **Página 404.** Existe, qué devuelve (código de estado real) y qué muestra.
11. **Metas sociales.** Open Graph y Twitter Cards de cada plantilla. Se
    pierden en casi todos los rediseños, y son cómo se ve la web al
    compartirla por WhatsApp o LinkedIn.
12. **Señales locales**, si el negocio es local: nombre, dirección y teléfono
    tal como aparecen y dónde, mapa embebido si lo hay, schema
    LocalBusiness/ProfessionalService, breadcrumbs si existen.

## Parte 2 · Lo que da dinero (aquí es donde duele perder algo)

13. **Formularios.** Cada formulario: a dónde envía, qué campos tiene, qué
    validación hace, qué pasa tras enviarlo (mensaje, redirección, email).
14. **Captación.** Suscripciones a newsletter y sus integraciones (servicio
    externo, API keys referenciadas, listas, CRM si lo hay).
15. **Pagos.** Si hay pasarela de pago: el flujo completo, paso a paso, desde
    el botón hasta la confirmación. Qué servicio, qué se envía, qué vuelve.
16. **Analítica y píxeles.** Todos los códigos de seguimiento instalados
    (Analytics, píxeles de redes, Search Console, Tag Manager), en qué páginas
    están, y los eventos de conversión configurados (envío de formulario, clic
    en teléfono, reserva): no solo los códigos, también qué miden. Se caen en
    cada rediseño del mundo y nadie lo nota hasta el mes siguiente.
17. **Cookies y consentimiento.** Qué banner hay, qué bloquea hasta aceptar,
    qué textos legales enlaza. Las páginas legales (aviso legal, privacidad,
    cookies) entran al inventario como lo que son: material factual — se
    migran tal cual o las renueva el usuario, nunca las redacta el agente.
18. **Correos transaccionales.** Qué emails manda la web (confirmaciones,
    avisos del formulario), desde qué dirección y por qué vía (SMTP, API,
    función del servidor).
19. **Antispam.** reCAPTCHA u otro sistema: versión, claves referenciadas, en
    qué formularios actúa.
20. **Citas y contacto rápido.** Calendarios de reserva embebidos (Calendly y
    similares), botones de WhatsApp, click-to-call, chats en vivo: qué script
    cargan, en qué páginas, y a qué número o URL derivan. En una web de
    servicios esto suele ser la vía de captación principal, y no aparece si
    solo se buscan «formularios».
21. **Prueba social embebida.** Reseñas de Google u otros widgets que carguen
    de un servicio externo: de dónde vienen y dónde se muestran.

## Parte 2b · El servidor (esto el usuario no tiene por qué saberlo)

El usuario normal no sabe si su hosting usa Apache, nginx o LiteSpeed, y no
pasa nada: no se lo preguntes, averígualo tú. Importa por una razón muy
concreta: decide **dónde se escriben las redirecciones, las cabeceras y el
forzado de HTTPS** de la web nueva. Una regla escrita en un fichero que el
servidor ignora no da error: simplemente no hace nada.

22. **Qué servidor sirve la web.** Pistas, de más a menos fiable: si existe
    `.htaccess` en el código descargado **y sus reglas se cumplen en la web
    publicada** (una redirección definida ahí que funciona al pedirla con
    `curl -sI` demuestra que el servidor lo respeta), las cabeceras de una
    respuesta real (`Server`, `x-powered-by` y compañía), y la documentación
    pública del hosting que te dijo el usuario en el paso 0. Conclusión que
    va al inventario, con su prueba: en Apache y LiteSpeed el `.htaccess`
    funciona; en nginx se ignora en silencio y la configuración real vive
    donde el usuario no llega por FTP — ahí las redirecciones irán por el
    panel del hosting o por PHP.
23. **Proxies y CDN por delante.** Comprueba si hay un Cloudflare u otro CDN
    delante (cabeceras `cf-ray` / `x-cache`, los DNS del dominio). Si lo hay,
    parte de las redirecciones, la caché y el certificado pueden vivir ahí y
    no en el hosting: hay que saberlo antes de tocar nada, y habrá que purgar
    su caché al publicar.
24. **Caché y compresión.** Qué capas de caché están activas hoy (plugin,
    caché del hosting, CDN) y qué cabeceras sirven páginas y assets
    (`Cache-Control`, `Expires`, gzip/brotli). La web nueva no puede servirse
    peor que la vieja.
25. **HTTPS y dominio canónico.** Cómo se fuerza hoy el HTTPS y la versión
    con o sin www, y en qué mecanismo vive esa redirección (¿.htaccess?
    ¿panel? ¿CDN?). Es la redirección que más veces se pierde sin que nadie
    la eche de menos hasta que Google duplica la web entera.

## Si la web actual es un WordPress

Además de todo lo anterior:

- Lista los plugins activos y qué hace cada uno de cara al público (SEO,
  formularios, caché, seguridad). Las redirecciones y los schemas suelen vivir
  en plugins, no en el tema.
- Tipos de contenido personalizados: identifica los Custom Post Types, sus
  taxonomías y los campos personalizados (ACF o similar) donde viva contenido
  real — casos de éxito, equipo, portafolio, testimonios. Si solo miras
  «páginas y entradas», te dejas media web de servicios fuera.
- Identifica dónde está definido cada contenido: qué es del tema, qué de un
  page builder y qué de la base de datos. Si el contenido lleva shortcodes del
  maquetador ([vc_row] y similares), lístalos: habrá que limpiarlos en la
  migración sin perder el texto ni su jerarquía.
- Documenta la configuración del plugin de SEO (titles, plantillas de metas,
  redirecciones, sitemap) exportándola o copiándola, porque no viaja sola.

## Parte 3 · Lo que la web no cuenta (contraste con la entrevista)

Que haya una web que auditar no significa que la web esté completa. Con el
inventario técnico hecho, contrasta el **contenido** de la web contra los
puntos 1 a 7 de `1-entrevista.md`, como si la web fuera la respuesta del
negocio a esa entrevista: ¿queda claro qué vende y a quién? ¿el «por qué él»
tiene pruebas (años, casos, cifras)? ¿hay material real (testimonios con
nombre, casos) o huecos? ¿cada página tiene clara la acción que pide al
visitante, y en la portada esa acción y la propuesta de valor se ven en el
primer pantallazo o hay que ir a buscarlas? ¿la prueba social está donde se
toma la decisión o escondida? ¿se explica cómo se trabaja con él (proceso,
plazos, objeciones)?

Cada hueco que encuentres va a `docs/MEJORAS.md` marcado **[CONTENIDO]**, en
una línea como el resto: qué falta, qué gana si se arregla, qué costaría.
No entrevistes todavía al usuario ni redactes nada: aquí solo se detecta. La
entrevista parcial, si él aprueba esas mejoras, ocurre en la fase 2.

## Formato de salida

`docs/INVENTARIO.md` con todas las partes, y al final una sección **RIESGOS**
con las tres cosas que más probabilidad tienen de romperse en este rediseño
concreto y por qué, citando el punto del inventario y el fichero donde viven.
Cada punto del inventario debe poder responderse después con «conservado /
roto / cambiado a propósito», y llevar una numeración estable: la fase 3 (y
las secciones CAMBIOS APROBADOS y [MEJORA]/[AMPLIACIÓN]) referenciarán los
puntos por su número, así que no se renumeran al añadir cosas — lo nuevo se
añade al final de su parte.

Y `docs/MEJORAS.md` con las carencias vistas por el camino: schemas que
faltan, titles flojos, páginas sin meta description, imágenes sin alt, sin
página 404 correcta, sin Open Graph… Es una lista de oportunidades, no de
tareas: **no arregles nada ni lo mezcles con el inventario**. El inventario
protege lo que hay; las mejoras son decisiones nuevas que tomará el usuario en
la fase 2. Cada mejora, en una línea: qué falta, qué gana si se arregla y
cuánto trabajo cuesta aproximadamente.

## Cierre de la fase

Presenta al usuario un resumen: cuántos puntos tiene el inventario, los tres
riesgos, y las mejoras encontradas. Dile que el siguiente paso es la fase 2, y
que empezará con sus decisiones, no con código.
