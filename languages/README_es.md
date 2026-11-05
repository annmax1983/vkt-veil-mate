# VKT VeilMate

[English](../README.md) | [中文](README_zh.md) | [Deutsch](README_de.md) | Español | [日本語](README_ja.md) | [Français](README_fr.md)

Una cortina para el navegador: una pulsación cubre todas las pestañas y, al desbloquear, todo vuelve a estar como estaba — nada se recarga, no se pierde ningún formulario, ningún vídeo se corta.

> Chrome · Edge · Firefox · Manifest V3 · Permisos mínimos · Sin analíticas · 100 % local

---

## ¿Por qué VKT VeilMate?

Sales a por un café. Alguien echa un vistazo a tu pantalla: un correo a medias, una pestaña del banco, un mensaje privado. Lo que quieres es una manta para tapar el navegador, no un producto de seguridad.

Las extensiones de «bloqueo del navegador» suelen hacer mal una de dos cosas:

| Su enfoque | Lo que falla |
|---|---|
| Llevar cada pestaña a una página de bloqueo | Al desbloquear se recarga todo: formularios perdidos, el vídeo vuelve a empezar, el estado de la SPA destruido |
| Prometer que «impide el acceso no autorizado» | Un perfil nuevo, una ventana privada o el administrador de tareas pasan por encima, y las reseñas lo dicen |

VKT VeilMate adopta la posición contraria:

| Nuestro enfoque | Resultado |
|---|---|
| **Cubrir, nunca navegar** — se inyecta una capa de shadow DOM en cada página | Desbloquear es instantáneo y sin pérdidas |
| **Decir lo que no puede hacer** — en la página de ajustes y en la ficha de la tienda | Sin expectativas defraudadas ni reseñas de una estrella por una promesa que nadie puede cumplir |
| **Sin camino de vuelta** — sin código de recuperación, sin endpoint de restablecimiento, y el bloqueo sobrevive al reinicio del navegador | Una cortina que se puede rodear no es una cortina; olvidar la contraseña obliga a eliminar la extensión, y cada pantalla lo dice |

---

## Funciones

### 🆓 Gratis para siempre

| Función | Detalle |
|---|---|
| Bloqueo con una pulsación | Botón de la barra de herramientas; no se registra ningún atajo de teclado |
| Lista de excepciones | Hasta 10 dominios siguen legibles; el resto queda cubierto |
| Capa sin pérdidas | Cada pestaña http/https se cubre en su sitio; nada se recarga |
| Bloqueo de interacción | En las páginas cubiertas se detienen clics, desplazamiento, teclado, arrastre, copia y menú contextual; al bloquear, el foco vuelve a la capa para que las pulsaciones no acaben en un editor dentro de un iframe |
| Nuevas pestañas y barra de direcciones | Las pestañas nuevas, las ventanas nuevas y las URL escritas se interceptan mientras está bloqueado |
| Desbloqueo por contraseña | PBKDF2-SHA256, 310.000 rondas, sal aleatoria, comparación en tiempo constante |
| Bloqueo que permanece | El estado vive en `storage.local`; reiniciar el navegador no lo levanta |
| Sin ruta de recuperación | Eliminar la extensión en `chrome://extensions` es la única salida si olvidas la contraseña |
| Bloqueo por inactividad | Usa la detección de inactividad del propio navegador |
| Espera creciente | Cinco fallos → 30 segundos, después 2 minutos, 10 minutos, 30 minutos y 1 hora. Toda comprobación de contraseña — desbloquear o cambiarla — suma en el mismo contador |
| Títulos de pestaña ocultos | Con el bloqueo activo, la barra de pestañas y el título de la ventana muestran un nombre neutro en lugar de la página que leías |
| Menú contextual | Bloquear todo o mantener legible el sitio actual, sin abrir el panel |
| Reloj grande | Reloj grande en la pantalla de bloqueo, 12/24 horas, fecha opcional |
| Seis idiomas | English, 中文, 日本語, Deutsch, Español, Français |

### ⭐ Pro (requiere licencia)

| Función | Detalle |
|---|---|
| Bloqueo dirigido | Cambia la lista de dominios a «cubrir solo…»: bloquea la intranet y deja legible lo demás. También desde el menú contextual. La versión gratuita se limita a 10 dominios y siempre funciona como «cubrir todo excepto…» |
| Bloqueo a una hora fija | Cubre todo a la hora que elijas, cada día o solo de lunes a viernes. Una alarma única que se reprograma tras cada disparo; si el navegador estaba cerrado, la hora perdida no bloquea al arrancar |
| Ventana sin contraseña | Unos minutos después de un desbloqueo real, un nuevo bloqueo se puede deshacer sin escribir la contraseña. El atajo no se renueva solo, un reinicio del navegador siempre la pide y cambiar la contraseña lo invalida al instante |
| Desbloqueo biométrico | Windows Hello / Touch ID mediante WebAuthn, con la contraseña siempre como alternativa. **Un atajo para no escribir, no una segunda llave**: la comprobación ocurre en la pantalla de bloqueo y quien abra DevTools ahí puede enviar el mismo mensaje — el mismo nivel que alguien delante del teclado. El límite sigue siendo la contraseña |
| Bloqueo al perder el foco | Bloquea unos segundos después de cambiar a otra aplicación |
| Vínculo con el bloqueo del sistema | Sigue el bloqueo de pantalla del sistema operativo |
| Bloqueo al iniciar el navegador | Pide la contraseña la primera vez que se abre el navegador |
| Cortina de privacidad | Difumina la página actual sin bloquear; una pulsación la descubre |
| Página señuelo | Las páginas cubiertas parecen un «No se puede acceder a este sitio» normal en lugar de una pantalla de bloqueo evidente; «Recargar» lleva a la pantalla de bloqueo |
| Registro de bloqueos | Historial local de los intentos de desbloqueo en este dispositivo, incluidas las comprobaciones hechas desde el formulario de cambio de contraseña |
| Fondo de pantalla y mensaje | Seis degradados incluidos o tu propia imagen, más una línea personalizada en la pantalla de bloqueo |
| Sincronización entre dispositivos | El aspecto de la pantalla de bloqueo, el reloj, las preferencias de bloqueo automático **y la lista de dominios** viajan por `chrome.storage.sync` (Chrome con Google, Edge con Microsoft, Firefox con Firefox Sync). Los cambios se envían solos un momento después de guardarlos y se reciben en cuanto el otro equipo escribe. La contraseña nunca se sincroniza; una imagen subida supera la cuota de 8 KB por elemento, así que solo viajan los degradados incluidos |

---

## Vista previa

> 📸 El material de la tienda y las capturas están en [`screenshots/`](../screenshots/): seis capturas de 1280×800 más las imágenes promocionales de 1400×560 y 440×280.

| Captura | Muestra |
|---|---|
| [`01-lock-all-tabs.png`](../screenshots/01-lock-all-tabs.png) | Una pulsación cubre todas las pestañas de todas las ventanas |
| [`02-lock-screen.png`](../screenshots/02-lock-screen.png) | Desbloqueo en la pantalla de bloqueo con el reloj grande |
| [`03-popup.png`](../screenshots/03-popup.png) | La ventana emergente: bloquear, definir contraseña, estado Pro |
| [`04-auto-lock-scope.png`](../screenshots/04-auto-lock-scope.png) | Bloqueo por inactividad y alcance del bloqueo (lista de dominios) |
| [`05-honest.png`](../screenshots/05-honest.png) | La tabla «puede / no puede» |
| [`06-security.png`](../screenshots/06-security.png) | Ajustes de contraseña y biometría |

---

## Navegadores compatibles

| Navegador | Estado | Versión mínima | Notas |
|---------|--------|----------------|-------|
| Google Chrome | ✅ Totalmente compatible | Chrome 116+ | Manifest V3, service worker |
| Microsoft Edge | ✅ Totalmente compatible | Edge 116+ | Misma compilación, basada en Chromium |
| Otros navegadores Chromium (Brave, Vivaldi, Opera) | ⚠️ Mejor esfuerzo | Chromium 116+ | Sin probar; usa las mismas API |
| Mozilla Firefox | ✅ Compatible | Firefox 121+ | Compilación MV3 mantenida en el repositorio dedicado de Firefox |
| Navegadores móviles | ❌ No compatibles | — | No hay barra de herramientas que pulsar ni modelo de ventanas que cubrir |

> **Windows Hello / Touch ID** dependen del soporte WebAuthn de la plataforma: Windows 10 1903 o posterior con PIN o huella configurados, o macOS con Touch ID. La contraseña siempre está disponible, así que un equipo sin biometría solo pierde comodidad.

---

## Instalación

| Tienda | Enlace |
|---|---|
| Chrome Web Store | 🔜 En revisión — el enlace se añadirá al publicarse |
| Microsoft Edge Add-ons | 🔜 En revisión — el enlace se añadirá al publicarse |
| Firefox Add-ons (AMO) | [Instalar para Firefox](https://addons.mozilla.org/firefox/addon/vkt-veilmate/) |

> Instala solo desde las tiendas oficiales indicadas arriba.

---

## Uso

### Primera configuración

1. Pulsa el icono de la barra → **Definir contraseña**. No hay código de recuperación: apunta la contraseña en un lugar seguro.
2. Pulsa **Bloquear ahora** cuando te levantes.
3. Desbloquea en la pantalla de bloqueo con la contraseña o, en Pro, con biometría.

### Configurar el alcance del bloqueo

Los dominios se comparan por sufijo con frontera de punto: `example.com` cubre `example.com`, `www.example.com` y `a.b.example.com`, pero no `notexample.com`. El esquema, el `www.` inicial, la ruta, el puerto y un prefijo comodín se eliminan automáticamente; un `com` suelto se rechaza.

Las páginas sin nombre de host (`chrome://`, `file://`, `about:blank`, PDF locales, páginas de extensiones) se cubren siempre, diga lo que diga la lista: la lista solo se aplica a http y https.

### Si olvidas la contraseña

Solo hay un camino: **eliminar la extensión en `chrome://extensions` y volver a instalarla.**

Eso borra también el fondo de pantalla y todos los ajustes. No hay código de recuperación, ni endpoint de restablecimiento, ni soporte capaz de desbloquearte: un candado con puerta trasera no es un candado. Cerrar el navegador tampoco ayuda: el estado vive en `storage.local` y sigue ahí tras reiniciar.

El panel «contraseña olvidada» de la pantalla de bloqueo enlaza directamente a `chrome://extensions/?id=<esta extensión>`, así que nunca te quedas sin salida, solo sin atajo.

---

## Cómo funciona

```
Disparador (botón / menú contextual / inactividad / pérdida de foco / bloqueo del sistema / inicio / hora fija)
  → estado de bloqueo escrito en storage.local (sobrevive al reinicio del navegador)
  → para cada pestaña http(s): tabs.sendMessage({type:'veil:lock'}) → se inyecta la capa
  → para pestañas que no admiten inyección: se recuerda la URL, tabs.update(lock.html)
  → tabs.onCreated / tabs.onUpdated siguen interceptando lo que aparece
  → windows.onCreated cubre Ctrl+N, «abrir en ventana nueva» y las ventanas privadas
  → chrome://extensions/?id=<propia> es la única página interna permitida, para que
    la extensión siempre pueda eliminarse
Desbloqueo
  → contraseña / WebAuthn verificados en la página de la extensión
  → se limpia el estado, se retiran las capas, las pestañas sustituidas vuelven a su sitio
```

Decisiones de diseño que conviene conocer:

- **Las contraseñas solo se escriben en páginas de la extensión.** El JavaScript de una web nunca ve el campo, así que ningún sitio puede capturarlo.
- **El hash se calcula en el service worker.** Solo se guarda `{salt, iter, hash}`; la contraseña nunca se escribe en ningún sitio.
- **Comparación en tiempo constante.** La comparación de hashes no filtra información de tiempo.
- **La capa vive en un shadow root cerrado.** Los scripts de la página no entran ni pueden reestilizar su interior. El elemento anfitrión sí está en el documento, así que una hoja de estilos del sitio puede apuntarle — por eso las propiedades críticas se escriben con `!important` en línea, y un guardián la repone si desaparece o se oculta.

---

## Preguntas frecuentes

**¿El bloqueo aguanta que cierre el navegador?** Sí. El estado se guarda en `storage.local`, así que el navegador se abre bloqueado hasta que desbloquees.

**¿Es un producto de seguridad?** No. Oculta pestañas de quien pasa por delante. Quien controle el equipo puede desactivarla en `chrome://extensions`, usar otro perfil o cerrar el navegador desde el administrador de tareas. Todo eso figura también en la ficha de la tienda.

**¿Por qué no hay recuperación de contraseña?** Un código de recuperación es una segunda llave, y una segunda llave es una puerta trasera. La única salida es eliminar la extensión, y está documentado en la propia pantalla de bloqueo.

**¿La biometría es una segunda entrada?** Es un atajo, no una segunda llave. La comprobación de la contraseña vive en el service worker, y los dos sitios donde se envía una contraseña — desbloquear y cambiar la contraseña — pasan por el mismo contador y la misma espera. La ventana sin contraseña no comprueba ninguna contraseña: solo vale unos minutos después de un desbloqueo real y deja una entrada `quick` en el registro. Pero quien pueda abrir DevTools en una página de la extensión puede manejar su propia API de mensajes, y ninguna extensión lo impide. Piensa en la biometría como «escribir menos», no como «más seguridad».

**¿Qué pasa tras el quinto fallo?** Una pausa de 30 segundos, luego 2 minutos, 10 minutos, 30 minutos y por último una hora entre intentos. El contador es por dispositivo y se ve en el registro de bloqueos.

**¿Sube algo?** Ni contenido de páginas, ni URL, ni pulsaciones, ni capturas. La única petición saliente es la activación o validación de la licencia.

**¿Por qué la versión gratuita limita la lista a 10 dominios?** El modo gratuito es «cubrir todo excepto…»: una lista corta cubre el caso realista (correo web, calendario, la página que estás leyendo). El modo inverso, «cubrir solo…», es lo que necesita un portátil de trabajo y forma parte de Pro.

**¿Puedo usar una licencia en dos navegadores?** Sí, una licencia activa dos navegadores y, al retirarla de uno, esa plaza vuelve a quedar libre.

---

## Privacidad

- Sin analíticas, sin telemetría, sin anuncios, sin cuentas.
- Ningún contenido de página, URL, título o pulsación sale del navegador.
- El fondo de pantalla y el mensaje se quedan en tu dispositivo: las imágenes que subes se redimensionan y se guardan en este perfil del navegador, nunca se envían.
- La sincronización entre dispositivos (Pro) usa `chrome.storage.sync`, el canal propio del navegador. En ese camino no hay servidor nuestro y no podemos leerlo. La contraseña queda deliberadamente excluida y las imágenes subidas superan la cuota, así que solo viajan los campos de preferencias.
- La única petición de red es la activación o validación de la licencia, y solo si pegas una clave.

- [Política de privacidad completa](https://annmax1983.github.io/vkt-veil-mate/privacy-policy.html)

### Permisos

| Permiso | Para qué |
|---|---|
| `storage` | Guardar ajustes (solo hashes), el estado persistente del bloqueo y los datos de Pro vía `storage.sync` |
| `tabs` | Cubrir pestañas e interceptar pestañas nuevas y direcciones escritas mientras está bloqueado |
| `windows` | Reaccionar a los cambios de foco para el bloqueo por pérdida de foco |
| `idle` | Bloqueo automático por inactividad |
| `alarms` | El bloqueo a una hora fija y el bloqueo diferido al perder el foco, sin depender de que el servicio de fondo siga despierto |
| `contextMenus` | El menú contextual (bloquear todo / mantener este sitio legible) |
| `https://api.annmax1983.com/*` | Solo activación y validación de la licencia |

Los content scripts se ejecutan en `http://*/*` y `https://*/*` y hacen exactamente una cosa: pintar la capa cuando el service worker se lo pide.

---

## Aviso de derechos de autor

1. VKT VeilMate cubre las páginas del propio navegador en tu dispositivo y no modifica, almacena ni transmite el contenido de ningún sitio web.
2. Los derechos de autor del contenido cubierto pertenecen a sus editores; VKT VeilMate no reclama ninguno.
3. Al usar esta extensión debes cumplir la legislación local y las políticas de dispositivo y uso aceptable de tu organización.

---

## Aviso sobre el código fuente

> ⚠️ **Este repositorio se mantiene para el desarrollo y el empaquetado de versiones.** El código es propietario y no puede redistribuirse ni reempaquetarse. La extensión se distribuye a través de las tiendas oficiales de navegadores (Chrome Web Store, Microsoft Edge Add-ons, Firefox Add-ons (AMO)); no se ofrecen paquetes de instalación offline a los usuarios finales.

---

## Licencia

Copyright © 2026 VKT VeilMate. Todos los derechos reservados.

Este software es software propietario de código cerrado. Sin autorización oficial por escrito queda estrictamente prohibido:
- Descompilar, crackear o modificar el código del programa
- Reempaquetar, redistribuir, compartir o revender comercialmente
- Incrustar el programa en otro software para distribuirlo en paquetes

---

## ❤️ Apoya el proyecto

Si VKT VeilMate te resulta útil, invita al desarrollador a un café.

**[👉 Obtener una licencia](https://annmax1983.com/extensions/veilmate)** · **[☕ Invítame a un café](https://ko-fi.com/annmax?ref=vkt-veil-mate)** · [Código en GitHub](https://github.com/annmax1983/vkt-veil-mate) · [Sitio oficial](https://annmax1983.com/)
