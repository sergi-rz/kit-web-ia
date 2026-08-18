# web-vieja/ — la web actual, descargada

Aquí vive la copia del código de la web que se va a sustituir (y el export de
su base de datos, si la tiene). La descarga el agente en la fase 1, o la deja
el usuario a mano. Si el proyecto es una web desde cero, esta carpeta se queda
vacía.

Reglas para cualquier agente que trabaje aquí:

1. **Solo lectura.** Nada de esta carpeta se modifica, nunca. Es la referencia
   contra la que se audita y desde la que se migra contenido.
2. **Contiene secretos.** El código descargado puede traer credenciales dentro
   (un `wp-config.php` lleva las claves de la base de datos; puede haber
   claves SMTP, de reCAPTCHA, de pasarelas). No se citan en respuestas, no se
   copian a `docs/` ni a `web-nueva/`, no se versionan.
3. **No se sube a ningún sitio.** Ni a un servidor, ni a un repositorio
   público, ni a ningún servicio externo.
