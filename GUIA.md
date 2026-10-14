# Guía paso a paso – Plataforma de Evaluaciones SIRAK

## Archivos
- `Codigo.gs` → va en Google Apps Script (NO se sube a GitHub: contiene la clave inicial).
- `index.html` y `logo.png` → se suben a GitHub.

## 1. Backend (Google Apps Script)
1. Cree una Hoja de cálculo de Google nueva ("SIRAK Evaluaciones"). Ahí quedarán todas las respuestas.
2. Menú **Extensiones → Apps Script**. Borre el contenido y pegue todo `Codigo.gs`. Guarde.
3. En el selector de funciones elija **setup** y pulse **Ejecutar**. Acepte los permisos (Avanzado → Ir a proyecto). Se crean las hojas, la administradora y la evaluación del Word.
4. **Implementar → Nueva implementación → Tipo: Aplicación web**. Ejecutar como: *Yo*. Quién tiene acceso: *Cualquier usuario*. Implementar y copie la **URL** (termina en /exec).
5. Si modifica `Codigo.gs` después: Implementar → Administrar implementaciones → editar → Nueva versión.

## 2. Frontend (GitHub)
1. Abra `index.html` y reemplace `PEGAR_AQUI_URL_DE_APPS_SCRIPT` por la URL del paso 1.4.
2. En github.com cree un repositorio (ej. `evaluaciones-sirak`) y suba `index.html` y `logo.png`.
3. **Settings → Pages → Branch: main / (root) → Save**. En 1–2 min su enlace será `https://SU-USUARIO.github.io/evaluaciones-sirak/`. Ese enlace se comparte con los funcionarios.

## 3. Primer ingreso
Usuario: `ecastillo` · Clave inicial: la indicada en el pedido. **Cámbiela de inmediato** (Mi cuenta) y luego borre la clave de `setup()` en Apps Script.

## 4. Uso
- **Usuarios**: crear, bloquear/desbloquear, asignar clave, eliminar. Solo la administradora principal crea administradores. "Olvidé mi clave" marca al usuario y usted le asigna una nueva.
- **Evaluaciones**: revise la clave de respuestas y el objetivo (son borrador), añada preguntas, guarde. No se puede guardar sin objetivo(s) y habilidad(es).
- **Horarios**: habilite inicio y término por persona o para todos.
- **Resultados**: ranking, revisión de preguntas de desarrollo (puntaje), retroalimentación y PDF.

## 5. IA con Groq (opcional, la activa el administrador)
1. En Apps Script abra `Codigo.gs`, en la función `configurarIA` reemplace `PEGAR_AQUI_CLAVE_GROQ` por la clave, ejecute `configurarIA` una vez y **borre la clave del código**. Queda guardada solo en Propiedades del script (nunca en GitHub).
2. La principal puede reemplazarla en **Mi cuenta → Clave de IA** (solo si es estrictamente necesario).
3. En un informe (Resultados → Revisar) aparecen "IA: sugerir puntaje de desarrollo" y "IA: analizar informe". Todo se revisa antes de guardar; el análisis puede pasar a la retroalimentación general. Se envía a la IA sin nombres.
4. Tras cambiar `Codigo.gs`: Implementar → Administrar implementaciones → editar → Nueva versión (la URL se mantiene).

## Solución al error "Cannot read properties of null (reading 'getSheetByName')"
Ocurre cuando el script no está vinculado a una Hoja de cálculo. El nuevo `Codigo.gs` lo resuelve: al ejecutar `setup` crea (o detecta) la hoja y guarda su ID. Pasos: pegar el nuevo código → ejecutar `setup` (aceptar permisos) → ver la hoja creada en Registro de ejecución o en su Google Drive ("SIRAK Evaluaciones - Respuestas") → Implementar → Administrar implementaciones → editar → Nueva versión.

## 6. Novedades: claves automáticas, correo, importar instrumentos y PDF con pauta
- **Actualizar:** pegar el nuevo `Codigo.gs` → ejecutar **setup** de nuevo (es seguro: agrega la columna "correo" y pide el permiso de correo) → Nueva versión de la implementación → subir el nuevo `index.html` a GitHub.
- **Claves automáticas:** en Usuarios deje la clave vacía (o use "Asignar clave" vacío) y se genera una de 10 caracteres. Se muestra una sola vez y, si marca "Enviar por correo", se envía desde la cuenta de Google que implementó el script. Límite aprox.: 100 correos/día en Gmail personal. El usuario debe cambiarla en su primer ingreso.
- **Importar Word/PDF:** Evaluaciones → "Importar Word/PDF con IA". Se lee el archivo, la IA arma el borrador (preguntas, tipos, clave propuesta, habilidades) y usted lo revisa y guarda. Funciona con archivos de hasta ~24.000 caracteres; sobre eso, dividirlos. Si prefiere, también puede enviarme el archivo por el chat para que yo lo prepare.
- **PDF del instrumento:** en Evaluaciones, "PDF con pauta" (clave, habilidad y puntaje por pregunta) y "PDF sin pauta" (hoja para aplicar en papel). Ambos con logo.

## 7. Horarios y velocidad (versión actual)
- Los horarios se guardan ahora como hora exacta de Chile (zona America/Santiago), sin depender de la hora del navegador ni de la hoja. Las habilitaciones antiguas se siguen leyendo; si alguna falla, quítela y vuelva a habilitarla.
- La pestaña y el título de "Horarios" pasaron a **Habilitar instrumentos**.
- Velocidad: lectura en caché, guardado de respuestas en bloque y bloqueo solo en acciones de administración. Aparece "Cargando…" mientras se procesa. Apps Script de por sí tarda 1–3 s por acción.
- Para actualizar: pegar `Codigo.gs` → Nueva versión de la implementación → subir `index.html` a GitHub (y refrescar con Ctrl+F5).

## 8. Novedades (14-oct): rendición, varios usuarios, IA y guardado
- **Cómo actualizar (siempre en este orden):** 1) pegar `Codigo.gs` completo en Apps Script y guardar; 2) ejecutar la función **`autorizar`** (acepte los permisos; solo la primera vez que se actualiza); 3) Implementar → Administrar implementaciones → editar → **Nueva versión**; 4) subir `index.html` a GitHub y refrescar con **Ctrl+F5**. Junto al título de la página aparece la versión (ej. `v14-oct-c`): si no la ve, el navegador o GitHub Pages aún muestran el archivo antiguo (puede tardar 1–2 min).
- **Rendición:** al pulsar Comenzar aparece una pantalla previa; el botón "Comenzar en pantalla completa" oculta las pestañas. Si la persona sale, un clic la vuelve a poner. Las preguntas se numeran como en el instrumento, con barra de avance por sección.
- **Varios usuarios a la vez y no perder respuestas:** guardado automático a los pocos segundos de cada respuesta (más respaldo en el equipo) y reintentos automáticos si falla la conexión. Si cierra la página, al volver a ingresar continúa donde quedó (el tiempo sigue corriendo).
- **Justificar falsas:** al marcar Falso aparece el recuadro "Justifique por qué es falso". En el editor, el botón "Pedir justificación en todas las V/F" la activa en todo el instrumento.
- **Perfiles de apoyo:** solo la administradora principal los crea (Usuarios → Perfil "Perfil de apoyo (evaluador)"). Pueden revisar resultados y usar la IA; no pueden crear ni eliminar.
- **IA (Groq):** el botón "IA: corregir todo" revisa V/F, alternativas y desarrollo, de a 5 preguntas, y prueba un segundo modelo si el primero falla. Todo se revisa antes de pulsar "Guardar revisión".
- **Si la IA dice "no configurada":** en Apps Script, función `configurarIA`, reemplace `PEGAR_AQUI_CLAVE_GROQ` por la clave, ejecútela, **vuelva a poner el texto original y guarde** (la clave queda solo en Propiedades del script). Luego ejecute `autorizar` y cree una Nueva versión.
- **Clave de IA y perfiles:** si la clave aún no está configurada, cualquier administrador puede pegarla en Mi cuenta → Clave de IA; para reemplazar una ya configurada se requiere la administradora principal (`ecastillo`). Arriba de Mi cuenta se muestra con qué usuario inició sesión.
- **Si los cambios de una evaluación "no quedan":** el servidor ahora lee siempre los datos frescos al abrir Evaluaciones y fuerza el guardado antes de liberar el bloqueo. Compruebe además que la versión de la página (junto al título) sea la última.
- **Informe del alumno (v14-oct-h):** el alumno solo lo ve en pantalla (sin botón de PDF) y **no ve el ranking ni su lugar**; eso es solo de la administración (el PDF de administración sí lo incluye). Si la administración desmarca "Mostrar la retroalimentación al alumno" al guardar la revisión, el alumno no ve ningún comentario.
- **Puntajes a mano:** en Resultados → Revisar, la administración y los perfiles de apoyo pueden cambiar el puntaje de **cualquier pregunta** (V/F, alternativas y desarrollo), también en informes ya revisados; pulse "Guardar revisión". Ojo: "Recalcular notas con la clave actual" reemplaza los ajustes manuales de V/F y alternativas.
- **Actualizar:** pegar `Codigo.gs` → ejecutar **`setup`** una vez (agrega la columna `verRetro`; es seguro) → Nueva versión de la implementación → subir `index.html`.
