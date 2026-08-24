# Fase 3 · Verificación contra el inventario, y publicación

Se entra aquí cuando la web nueva está terminada en `web-nueva/`. La fase tiene
tres pasos, en orden: la verificación del agente, las comprobaciones manuales
del usuario, y solo entonces la publicación.

## Paso 1 · La verificación del agente

Comprueba `docs/INVENTARIO.md` punto por punto contra la web nueva y devuelve
una tabla con tres columnas:

```
punto · estado · detalle
```

Estados posibles, solo estos tres:

- **CONSERVADO**: está igual que en el inventario. Cita dónde lo has
  comprobado.
- **ROTO**: falta o ha cambiado sin que sea una decisión. Di exactamente qué
  había, qué hay ahora y dónde.
- **CAMBIADO A PROPÓSITO**: ha cambiado y coincide con una entrada de la
  sección CAMBIOS APROBADOS del inventario. Referénciala. Si no hay entrada,
  es ROTO.

Los puntos marcados **[MEJORA]** y **[AMPLIACIÓN]** se comprueban igual que
el resto: en su día eran opcionales, pero al aprobarse se volvieron promesas.
Una mejora o ampliación aprobada y no implementada es ROTO, no «bueno, era un
extra».

Reglas:

- Nada de «parece correcto». Cada CONSERVADO lleva la prueba: la URL
  comprobada, el fichero leído, el valor encontrado.
- Si tu entorno permite ejecutar comandos, no verifiques solo leyendo código:
  levanta la web nueva en un servidor local (`php -S localhost:8000` basta
  para este stack), recorre las URLs del inventario comprobando su código de
  estado y los enlaces internos, y compara el peso de las imágenes críticas
  contra el inventario. Lo comprobado en vivo pesa más que lo deducido del
  código.
- Si alguna página usa **parámetros GET** (un `?enviado` de formulario, un
  token, un filtro), comprueba con peticiones reales que la respuesta CON el
  parámetro difiere de la respuesta sin él. Si son idénticas, lo más probable
  es que el catch-all del rewrite esté descartando la query string por falta
  del flag QSA (ver fase 2) — no un problema de caché.
- **Lo legal de serie** (fase 2) se comprueba, no se supone: en una carga
  limpia sin aceptar nada, ninguna petición ni cookie de analítica o píxeles
  (si hay banner, bloquea de verdad); cada formulario con datos personales
  lleva su casilla sin premarcar y la información de primera capa visible;
  y las páginas legales responden 200 y están enlazadas desde el pie.
- Comprueba las URLs de una en una contra la lista del inventario: código de
  estado de cada una y que el contenido corresponde. Las redirecciones del
  inventario siguen respondiendo 301 hacia su destino correcto.
- Compara los titles, descriptions y h1 contra la tabla del inventario, celda
  a celda.
- Para el texto que posiciona: confirma que el contenido de esas páginas es el
  del inventario. Si se reescribió algo, va como ROTO salvo que exista la
  aprobación.
- Los schemas: valida que cada plantilla emite los mismos datos estructurados,
  y pásalos por un validador de resultados enriquecidos si tienes forma.
- Metas robots: ninguna página puede haber quedado en noindex sin una entrada
  en CAMBIOS APROBADOS.
- Las metas sociales (Open Graph) siguen ahí.
- Abre las páginas clave y confirma que no hay errores de JavaScript en la
  consola ni saltos de maquetación evidentes al cargar.
- Analítica y píxeles: confirma que cada código del inventario está presente
  en las mismas páginas. Este es el punto que más veces vas a encontrar ROTO.
- Si la web venía de cero (entrevista): confirma además que ningún PENDIENTE
  del inventario se rellenó por el camino sin aprobación.
- Ordena la tabla con los ROTO primero, y dentro de los ROTO, primero lo que
  toca dinero o tráfico (pagos, formularios, URLs, noindex) y después el resto.

Y al final, una lista aparte: **«LO QUE NO HE PODIDO COMPROBAR»**, con el
motivo. No lo marques como conservado si no lo has visto.

Si hay ROTOS, se arreglan y se repite la verificación. A publicación no se
llega con ROTOS abiertos.

## Paso 2 · Lo que NO se delega (las pruebas del usuario)

Tres cosas se comprueban a mano, con el dedo, siempre. El agente puede leer el
código de un formulario y decir que está bien conectado, pero eso no es lo
mismo que el correo llegando a la bandeja. Pídele al usuario estas tres
pruebas y espera su confirmación:

1. **El formulario de contacto**: enviarlo de verdad y ver llegar el email.
2. **La captación**: suscribirse con un correo real y comprobar que entra en
   la lista.
3. **El pago**, si lo hay: una compra real, hasta el final, con el correo de
   confirmación entrando en pantalla.

Y mientras hace esas pruebas, que mire la analítica en tiempo real: los
eventos de conversión del inventario (envío, clic, compra) tienen que
registrarse. Un formulario que funciona pero no mide es media avería. Si la
web da de comer, esta media hora manual no es opcional.

(Estas pruebas pueden hacerse en el servidor sobre una subcarpeta o subdominio
de pruebas antes del cambio definitivo, si el usuario lo prefiere.)

## Paso 3 · Publicación

Solo con la verificación limpia y las pruebas manuales hechas:

- Al servidor se sube **únicamente el contenido de `web-nueva/`**. Nunca el
  kit entero (regla 4 del AGENTS.md).
- Si el usuario dio credenciales FTP en la fase 1, el agente puede hacer la
  subida — con su aprobación explícita en ese momento, no como parte
  automática de la fase. La alternativa: el usuario sube `web-nueva/` él
  mismo con su cliente FTP.
- **Antes de subir nada, confirma la carpeta de destino.** La ruta de la raíz
  de la web debería estar apuntada en `.secrets/` desde la fase 1; si no está
  o está en blanco, no des por hecho que la carpeta donde aterriza la conexión
  FTP es la buena — muchas cuentas entran en la home del servidor, no en la
  raíz que sirve el dominio. Demuéstralo antes de tocar nada: los ficheros de
  esa carpeta tienen que coincidir con lo descargado en `web-vieja/`, o, si el
  servidor está vacío, sube un fichero de prueba minúsculo y comprueba que
  responde en el dominio (y bórralo). Si no puedes demostrarlo, para y
  pregunta al usuario. Subir la web a la carpeta equivocada no da error: deja
  el dominio sirviendo lo viejo y los ficheros nuevos perdidos por el
  servidor.
- **La web vieja y la nueva no se mezclan.** Subir encima de lo que hay
  sobrescribe unos ficheros, deja otros obsoletos conviviendo con los nuevos,
  y limpiar eso después es un follón. En su lugar: mueve todo lo que haya en
  la carpeta raíz a una subcarpeta de archivo con fecha (por ejemplo
  `_web-anterior-AAAA-MM-DD/`, con la fecha del día) y sube el contenido de `web-nueva/` a la raíz
  ya vacía, todo seguido para que el corte sea mínimo. Así la web vieja queda
  localizada en un solo sitio, y el usuario decide luego si se la descarga o
  la borra — pero no se borra del servidor hasta que la nueva lleve unos días
  funcionando, y la copia de seguridad de la fase 1 no se toca en ningún caso.
  Esa subcarpeta cuelga de la raíz pública, así que hay que cerrarla al
  exterior: si el servidor respeta `.htaccess` (Parte 2b del inventario), un
  `Deny from all` dentro; si no, mejor moverla fuera de la raíz si la cuenta
  FTP alcanza un nivel por encima. Y no forma parte de la web nueva: queda
  fuera de la verificación y del sitemap.
- El camino prudente si el usuario quiere probar en el servidor antes del
  cambio: subir a una subcarpeta o subdominio de pruebas, revisar, y hacer el
  cambio definitivo al final (el archivado de la vieja se hace igual en ese
  momento).
- Tras el cambio, **purga todas las capas de caché del inventario** (caché
  del hosting, CDN si lo hay): el clásico «he subido la web nueva y sigue
  saliendo la vieja» casi siempre es esto, no un fallo de la subida.
- Y comprueba redirecciones, forzado de HTTPS y cabeceras de caché **con
  peticiones reales contra producción** (`curl -sI` a las URLs del
  inventario): en local no se puede saber si el servidor respeta el fichero
  donde están escritas (Parte 2b del inventario) — una regla ignorada no da
  error, simplemente no actúa.
- Repasa que robots.txt y sitemap apuntan a lo nuevo, y que ninguna URL del
  inventario responde distinto en producción de como lo hacía en la
  verificación.

## Después

La carpeta del kit se conserva entera: es el proyecto. Los cambios futuros se
piden abriendo el agente aquí — el inventario, las decisiones y el histórico
ya están en `docs/`, y la regla de conservación sigue aplicando: lo que la web
tiene hoy pasa a ser lo que no se puede perder mañana.
