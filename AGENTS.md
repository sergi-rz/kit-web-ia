# Kit para rehacer (o crear) tu web con un agente de IA

Este fichero es **la fuente de verdad del proyecto**. Cualquier agente que
trabaje en esta carpeta (Claude Code, Codex o equivalente) debe leerlo entero
antes de hacer nada, y volver a él ante cualquier duda. Las instrucciones de
cada fase están en `fases/` y complementan a este fichero; si algo entra en
conflicto, manda lo que diga aquí.

## Qué es esto

Un sistema para rehacer una web existente (o crear una desde cero) con IA
**sin perder nada de lo que hoy trae visitas o dinero**. No es un prompt: es
una carpeta de trabajo con directrices permanentes, tres fases y un rastro
escrito de todas las decisiones. La carpeta entera es el proyecto, y se
conserva después del lanzamiento: cualquier cambio futuro se pide abriendo el
agente aquí, con todo el contexto ya en los ficheros.

## La estructura

```
kit-web/
├── AGENTS.md        ← este fichero: las reglas del proyecto
├── CLAUDE.md        ← importa este fichero (para Claude Code)
├── fases/
│   ├── 1-auditoria.md    ← si HAY web previa que auditar
│   ├── 1-entrevista.md   ← si NO hay web previa (sustituye a la auditoría)
│   ├── 2-ejecucion.md    ← el desarrollo, con decisiones y mockups antes
│   └── 3-verificacion.md ← comprobar la web nueva contra el inventario
├── docs/            ← lo que el agente escribe: INVENTARIO, MEJORAS, DECISIONES, mockups
├── web-vieja/       ← el código y la BD de la web actual · SOLO LECTURA
├── web-nueva/       ← la web que se construye · LO ÚNICO QUE SE PUBLICA
└── .secrets/        ← credenciales (FTP, BD…) · ni se versiona ni se sube ni se cita
```

Cada fase se arranca diciéndole al agente: *«Lee AGENTS.md y empieza la fase X»*.

## Las reglas del proyecto

### 1 · El inventario manda

`docs/INVENTARIO.md` es la lista de lo que no se puede perder, y manda sobre
cualquier otra instrucción. Todo lo que está ahí se conserva. Si en algún
momento conviene cambiar algo del inventario (una URL, un texto, un schema),
no se cambia: se propone al usuario con el motivo y se espera su aprobación.
Cada cambio aprobado se apunta en la sección **CAMBIOS APROBADOS** al final
del propio INVENTARIO.md. Esa sección es la que separará después un «roto» de
un «cambiado a propósito».

### 2 · Nada factual se inventa

Datos del negocio, precios, cifras, testimonios, nombres de clientes: salen de
la web vieja o de las respuestas del usuario, o no existen. Los textos que ya
posicionan no se reescriben sin aprobación explícita. Un hueco sin material se
marca **PENDIENTE**, nunca se rellena con texto verosímil.

### 3 · Toda decisión se escribe

**Si una decisión no está escrita en `docs/`, no existe.** Las conversaciones
se compactan y las sesiones se cierran; los ficheros se quedan. Todo lo que se
decida (qué se conserva, qué mejoras se aprueban, qué dirección de diseño se
elige, qué stack, qué se descarta) se escribe en el momento en
`docs/DECISIONES.md`, con fecha y motivo. Una sesión nueva debe poder
continuar el proyecto leyendo solo `docs/` y este fichero.

### 4 · Seguridad y accesos

- Las credenciales (FTP, SSH, BD) viven en `.secrets/`, y solo ahí. No se
  versionan, no se suben a ningún sitio, no se pegan en ficheros de docs ni se
  citan en respuestas.
- `web-vieja/` es **solo lectura** y puede contener secretos dentro del propio
  código descargado (un `wp-config.php` trae las claves de la base de datos).
  No se modifica, no se sube a ningún sitio, y sus secretos no se copian a
  ningún otro fichero.
- La web en producción **no se toca** durante las fases 1 y 2. Publicar es un
  paso aparte, al final de la fase 3, con aprobación explícita del usuario.
- Al servidor se sube **únicamente el contenido de `web-nueva/`**. Nunca el
  kit entero: subir esta carpeta a un hosting público publicaría credenciales
  y documentación interna.
- Antes de cualquier trabajo sobre una web real: confirmar con el usuario que
  existe **copia de seguridad** de ficheros y base de datos.

### 5 · El stack estándar

La web nueva se construye con la opción más aburrida que funcione en un
hosting compartido normal:

- **Prácticamente estática**: HTML y CSS planos, JavaScript solo donde aporte.
- **PHP mínimo** y sin frameworks, solo para lo que lo necesite de verdad:
  configuración, textos compartidos (cabeceras, pies), rutas y procesamiento
  de formularios.
- **Base de datos opcional**, y solo si hay una razón concreta. Una web de
  servicios normalmente no la necesita.
- **Sin proceso de compilación**, sin gestores de dependencias, sin CMS.

El criterio: esta web la va a editar en el futuro una IA o una persona que no
la escribió, y eso lo facilita la tecnología simple. Si el agente cree que
este proyecto necesita más que esto, lo justifica por escrito y espera
aprobación. WordPress puede ser el **origen** (se audita y se migra desde él),
pero no es el destino de este kit.

### 6 · El agente pregunta, el usuario decide

En cada fase hay decisiones que son del usuario: qué conservar, qué mejorar,
qué dirección de diseño seguir. El agente es proactivo — pregunta en bloques
pequeños, acompaña cada pregunta de su recomendación razonada según lo que ha
analizado, y ofrece opciones concretas — pero no decide por él, y no avanza de
fase sin cerrar las decisiones de la anterior.

### 7 · Rendimiento y accesibilidad no son adornos

Imágenes con dimensiones declaradas y peso razonable, nada de scripts que
bloqueen el renderizado sin motivo, contraste AA en los textos, áreas táctiles
de 44px. Una web nueva que carga peor que la vieja es una web rota aunque sea
más bonita.

## Para quién NO es este kit

Antes de empezar, el agente lo comprueba con el usuario: si publica contenido
a diario desde un panel de administración y no piensa usar la IA para
editarlo, si otras personas no técnicas necesitan editar la web, o si es una
tienda con cientos de productos gestionada desde un backoffice — este kit no
es el camino, y hay que decírselo antes de que invierta tiempo, no después.
