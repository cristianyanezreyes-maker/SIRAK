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
