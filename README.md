# Kit Web IA

Un kit para rehacer tu web (o hacerla de cero) con un agente de IA — Claude
Code, Codex o equivalente — sin perder por el camino lo que hoy te trae
visitas o dinero.

Lo enseño en funcionamiento en este vídeo: **[PENDIENTE: enlace al vídeo]**.
Recomiendo verlo antes de usar el kit: cada proyecto tiene sus matices y ahí
explico cómo aplicarlo según tu caso.

## Cómo se usa

1. Descarga esta carpeta (botón *Code → Download ZIP*, o `git clone`).
2. Abre tu agente de IA dentro de la carpeta.
3. Dile: **«Lee AGENTS.md y empieza la fase 1»**.

A partir de ahí el propio agente te va guiando: qué necesita de ti (accesos,
copia de seguridad), qué va a auditar, y qué decisiones son tuyas.

## Qué hay dentro

```
kit-web-ia/
├── AGENTS.md        ← las reglas del proyecto (la fuente de verdad)
├── CLAUDE.md        ← la versión para Claude Code (importa AGENTS.md)
├── fases/
│   ├── 1-auditoria.md    ← si ya tienes una web que vas a sustituir
│   ├── 1-entrevista.md   ← si empiezas de cero, sin web anterior
│   ├── 2-ejecucion.md    ← decisiones, mockups y desarrollo
│   └── 3-verificacion.md ← comprobar que no se ha roto nada, y publicar
├── docs/            ← aquí escribe el agente: inventario, mejoras, decisiones
├── web-vieja/       ← aquí se descarga tu web actual (solo lectura)
└── web-nueva/       ← aquí se construye la nueva (lo único que se sube al servidor)
```

La idea de fondo: en vez de un prompt largo que se pierde cuando la
conversación se alarga, las directrices viven en ficheros que el agente
recarga siempre, y **toda decisión queda escrita** en `docs/`. La carpeta
entera es tu proyecto: guárdala, y los cambios futuros los pides abriendo el
agente ahí dentro, con todo el contexto.

## Para quién es (y para quién no)

Funciona bien para webs de servicios y corporativas: la típica web de un
freelance o un negocio local, tenga histórico de SEO que conservar o no. La
web resultante es prácticamente estática, con el mínimo PHP necesario, pensada
para un hosting compartido normal.

No es para ti si publicas contenido a diario desde un panel de administración
y no piensas usar la IA para editarlo, si otras personas no técnicas necesitan
editar la web, o si tienes una tienda con cientos de productos gestionada
desde un backoffice.

Y que nadie se confunda: este kit no te hace el trabajo de SEO. Lo que evita
es lo contrario — la web bonita sin base que te saca un prompt vago de una
línea. Con esto tienes un suelo sobre el que luego sí se puede trabajar.

---

Hecho por [Sergi Ruiz](https://sergiruiz.es) · cuento estas cosas en
[la newsletter](https://desdelacueva.sergiruiz.es/), en
[YouTube](https://www.youtube.com/@sergi-ruiz) y en
[X](https://x.com/sergi_rz).
