# Lo que llevas puesto — guía de la página

En este repositorio hay tres archivos:

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La página completa: Archivo, Historias y Mi cápsula. |
| `firestore.rules` | Las reglas de seguridad para copiar en Firebase. |
| `LEEME.md` | Esta guía. |

---

## 1. Publicar la página con GitHub Pages

1. En GitHub, toca el **+** de arriba → **New repository**.
2. En *Repository name* escribe `loquellevaspuesto`, déjalo en **Public**, marca **Add a README file** y toca **Create repository**.
3. Toca **Add file → Upload files**, elige los tres archivos y toca **Commit changes**.
4. Entra a **Settings → Pages**. En *Source* elige **Deploy from a branch**, en *Branch* elige **main** y **/(root)**, y toca **Save**.
5. Espera 1 o 2 minutos y recarga. Tu página queda en:
   **https://viuhxs.github.io/loquellevaspuesto/**

**Para actualizarla:** sube otra vez `index.html` con **Add file → Upload files**. El nuevo reemplaza al anterior y la página cambia en 1 o 2 minutos.

---

## 2. Conectar Firebase para que las historias se compartan

Sin este paso, la página funciona en **modo local** (aparece una franja beige arriba): cada historia publicada queda guardada solo en el celular de quien la escribió.

1. Entra a <https://console.firebase.google.com> con tu cuenta de Gmail y crea un proyecto, por ejemplo `lo-que-llevas-puesto`. Puedes desactivar Google Analytics.
2. En la página del proyecto, toca el ícono **`</>`** (Web) para agregar una app web. Ponle un nombre y toca **Registrar app**.
3. Firebase te muestra un bloque llamado `firebaseConfig`, parecido a este:
   ```js
   const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "lo-que-llevas-puesto.firebaseapp.com",
     projectId: "lo-que-llevas-puesto",
     storageBucket: "lo-que-llevas-puesto.appspot.com",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abc123"
   };
   ```
   Copia esos valores.
4. En el menú de la izquierda entra a **Compilación → Firestore Database → Crear base de datos**. Elige una ubicación cercana (por ejemplo `southamerica-east1`) y el **modo de producción**.
5. Dentro de Firestore abre la pestaña **Reglas**, borra lo que haya, pega todo el contenido de `firestore.rules` y toca **Publicar**.
6. Pon los valores del paso 3 en `index.html`. Busca `window.LQCP_FIREBASE_CONFIG` (cerca de la línea 740) y llena cada campo entre las comillas.
   *Si prefieres, pásale el bloque `firebaseConfig` a Claude y te devuelve el `index.html` ya conectado.*
7. Sube el `index.html` nuevo a GitHub. Cuando la franja beige de «Modo local» desaparezca, la página ya está conectada.

> Los datos de `firebaseConfig` no son una contraseña. Es normal que estén en la página. Lo que protege la información son las reglas del paso 5.

**Para moderar:** en Firestore Database → *stories* puedes ver todas las historias y borrar las que no quieras que aparezcan.

---

## 3. Agregar una cápsula nueva en «Historias»

1. Sube el video a YouTube como **Público** o **No listado** (no *Privado*).
2. En `index.html` busca `window.LQCP_CAPSULAS` y copia un bloque como este:
   ```js
   {
     titulo: "¿La pregunta de tu cápsula?",
     descripcion: "",
     youtube: "https://youtu.be/XXXXXXXXXXX"
   },
   ```
3. Cambia la pregunta y el link. **La primera cápsula de la lista aparece grande, como destacada.**
4. Sube el `index.html` actualizado a GitHub.

---

## 4. Datos de contacto en «Mi cápsula»

- Correo: viuibarra@gmail.com (en celular abre la app de Gmail)
- WhatsApp: +57 304 481 6991 (en celular abre la app de WhatsApp)

Para cambiarlos, busca `var CONTACT = {` en `index.html`. Cambia también los enlaces del botón **Quiero mi cápsula** (`id="mcMailBtn"`) y del botón **Escríbeme por WhatsApp** (`id="mcWaBtn"`).
