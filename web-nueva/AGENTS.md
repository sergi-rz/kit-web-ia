# web-nueva/ — la web que se construye

Aquí se monta la web nueva durante la fase 2. Empieza vacía y acaba siendo
**lo único que se publica**: subir el contenido de esta carpeta a un servidor
es todo lo que hace falta para que la web funcione.

Reglas para cualquier agente que trabaje aquí:

1. **Autocontenida.** Nada de aquí puede depender de ficheros de fuera de esta
   carpeta (ni de `docs/`, ni de `web-vieja/`, ni de rutas locales de la
   máquina). Si un recurso hace falta en la web, vive aquí dentro.
2. **Sin secretos en el código.** Las credenciales que la web necesite en el
   servidor (SMTP del formulario, claves de servicios) van en un fichero de
   configuración claramente separado y documentado — nunca esparcidas por el
   código, y nunca las del usuario que viven en `.secrets/`.
3. **El stack es el estándar del kit** (regla 5 del AGENTS.md raíz):
   prácticamente estática, PHP mínimo, BD solo con razón concreta, sin
   frameworks ni compilación.
4. **Los mockups no van aquí.** Las pruebas de diseño de la fase 2 viven en
   `docs/mockups/`; esta carpeta solo contiene lo que se publicará.
