# N2 Obra 2026 — Detección, CCTV y Voz y Datos

Versión nueva con su **propio script de Google** y su **propia carpeta en Drive**.
Lo anterior queda intacto: el script viejo, la carpeta «Fotos sensores - Nivel 02», sus
evidencias y la página MTY-Sen siguen funcionando igual.

```
N2-Obra-2026/
├── index.html             la página
├── config.js              aquí pegas la URL del script nuevo
├── plano-deteccion.png
├── plano-cctv.png
├── plano-vozydatos.png
├── LEEME.md
└── apps-script/
    └── Code.gs            el script nuevo (clave n2obran2026)
```

Las fotos nuevas quedan así en tu Drive:

```
Fotos N2 Obra 2026/
├── Detección de incendios/   S-N2DH14__20261031-101530__a1b2.jpg
├── CCTV/                     N2CAM04__20261031-102210__c3d4.jpg
└── Voz y Datos/              N2AP03__20261031-103005__e5f6.jpg
```

Las subcarpetas se crean solas con la primera foto de cada servicio.

---

## Parte 1 — Actualizar el código del script N2 Obra 2026

Ya tienes el proyecto **N2 Obra 2026** creado y publicado; solo hay que poner el código
correcto y publicar una versión nueva. **La URL no cambia.**

1. Entra a <https://script.google.com> y abre el proyecto **N2 Obra 2026**.
   **No abras ni toques el proyecto anterior.**
2. Haz clic dentro del editor, selecciona todo (**Ctrl+A**) y bórralo (**Supr**).
3. Abre `apps-script/Code.gs` de este paquete con el Bloc de notas, selecciona todo,
   copia y pégalo en el editor.
4. Revisa estas dos líneas:
   - línea 18: `const CLAVE = 'n2obran2026';`
   - línea 19: `const NOMBRE_CARPETA = 'Fotos N2 Obra 2026';`

   Si ves `obra2026` o `Fotos sensores - Nivel 02`, es el código viejo: repite los pasos 2 y 3.
5. Guarda con **Ctrl+S**.
6. En la lista de funciones (junto a **Ejecutar**) elige **prueba** y da clic en **Ejecutar**.
   Si pide permisos: **Revisar permisos → tu cuenta → Configuración avanzada →
   Ir a N2 Obra 2026 (no seguro) → Permitir**.
   Abajo debe aparecer «Carpeta lista: Fotos N2 Obra 2026».
7. Publica la versión nueva: **Implementar → Gestionar implementaciones →
   lápiz (editar) → Versión: Nueva versión → Implementar**.
   Revisa que siga diciendo **Ejecutar como: Yo** y **Quién tiene acceso: Cualquier usuario**.

## Parte 2 — Probar el script (no avances sin esto)

Abre esta dirección en el navegador:

```
https://script.google.com/macros/s/AKfycbwEZckvorUElQfVB5tNmTjLoMHZtnGGTHxIIGQRUpwR7RzonthC8zMBzSsLlGYvTfE-/exec?clave=n2obran2026
```

Debe salir:

```
{"ok":true,"fotos":{},"script":"N2 Obra 2026"}
```

Cómo leer lo que salga:

| Respuesta | Qué significa |
|---|---|
| `{"ok":true,…,"script":"N2 Obra 2026"}` | Todo bien, sigue a la Parte 3. |
| `{"ok":false,"error":"clave","script":"N2 Obra 2026"}` | El código es el nuevo pero la clave no es `n2obran2026`: revisa la línea 18 y publica nueva versión. |
| `{"ok":false,"error":"clave"}` **sin** `"script"` | Sigue publicado el código viejo: repite la Parte 1 completa, incluido el paso 7. |
| Página de Google pidiendo iniciar sesión o con error | La implementación no tiene acceso **Cualquier usuario**. |

## Parte 3 — Configurar la página

`config.js` **ya viene listo** con tu URL nueva y la clave `n2obran2026`. No necesitas
cambiar nada. Si algún día creas otro script, ahí es donde se pega su URL.

## Parte 4 — Subir a GitHub como repositorio nuevo

Así la página anterior (MTY-Sen) sigue funcionando con sus evidencias.

1. En GitHub da clic en **+ → New repository**. Nombre: **N2-Obra-2026**, **Public** →
   **Create repository**.
2. Da clic en **uploading an existing file** y arrastra:
   `index.html`, `config.js`, `plano-deteccion.png`, `plano-cctv.png`, `plano-vozydatos.png`
   (la carpeta `apps-script` no hace falta).
3. Da clic en **Commit changes**.
4. Ve a **Settings → Pages** → Source: **Deploy from a branch**, rama **main**,
   carpeta **/ (root)** → **Save**.
5. Espera unos 2 minutos. Tu página queda en:
   ```
   https://esilver221.github.io/N2-Obra-2026/
   ```
6. Ábrela en una **pestaña privada**. Debes ver **Detección 0/92**, **CCTV 0/25** y
   **Voz y Datos 0/26**, sin aviso amarillo.

## Parte 5 — Prueba antes de mandarlo a campo

En cada pestaña toca un dispositivo → **Tomar foto** → espera «Foto … guardada ✓».
Revisa que el círculo cambie a verde y que la foto aparezca en su subcarpeta de
**Fotos N2 Obra 2026**. Para quitar las fotos de prueba, bórralas en Drive.

Mándale al técnico la dirección **nueva**. La de MTY-Sen guarda en el script anterior.

---

## Funciones de la página

| Botón | Qué hace |
|---|---|
| Pestañas | Cambia entre Detección, CCTV y Voz y Datos. Muestran cuántos llevan foto. |
| **Capas y conteo** | Mostrar u ocultar etiquetas y elegir su tamaño, colorear por avance o por categoría, prender o apagar categorías y ver cuántos hay de cada una. |
| **Exportar plano PNG** | Descarga el plano con lo visible, las etiquetas (si están prendidas) y la tabla de conteo. |
| **Siguiente** | Lleva al siguiente dispositivo que falta. |
| Buscador | Busca por etiqueta (ej. `N2CAM04`) o por tipo (ej. `access`). |

## Cambiar una etiqueta sin perder sus fotos

Cada dispositivo en `index.html` tiene esta forma:

```js
["N2CAM04", "N2CAM04", "CAM", 0.32751, 0.53026]
//  clave     etiqueta   tipo   posición
```

- Cambia **solo el segundo texto** (la etiqueta que se ve) y las fotos siguen ligadas.
- Si cambias la clave, las fotos se desconectan (no se borran; se reconectan renombrando
  el archivo en Drive con la clave nueva al inicio).
- No toques los dos números del final.

## Si algo no funciona

| Lo que ves | Qué hacer |
|---|---|
| «Modo visor…» | `API_URL` está vacío en el `config.js` de GitHub. |
| «La clave … no coincide…» | `config.js` y `Code.gs` deben decir `n2obran2026`. Si editaste `Code.gs` después de implementar: **Implementar → Gestionar implementaciones → lápiz → Versión: Nueva versión**. |
| «No se pudo conectar con Google Drive» | La implementación debe decir **Cualquier usuario** y la URL terminar en `/exec`. |
| Las fotos caen en la carpeta vieja | La página está usando la URL del script anterior; revisa `API_URL`. |
| Se ve la página vieja | Ábrela en pestaña privada o espera a que **Actions** termine. |
