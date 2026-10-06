# 🎓 MentorApp

Plataforma web de **mentorías académicas y profesionales** que conecta a estudiantes con mentores (docentes y profesionales). Permite explorar perfiles, solicitar mentorías, chatear, organizar sesiones, compartir materiales y resolver dudas.

> Proyecto integrador — IESTP Manuel Scorza Torre (Acobamba, Huancavelica).

## ✨ Funcionalidades

| Rol | Qué puede hacer |
|---|---|
| **Estudiante** | Explorar mentores con filtros (especialidad, día, experiencia), solicitar mentorías, chatear, ver su cronograma, descargar materiales, pedir ayuda con dudas, calificar mentores, usar el centro de aprendizaje (temporizador Pomodoro) y seguir su progreso. |
| **Mentor** | Gestionar perfil y especialidades, definir disponibilidad, aceptar o rechazar solicitudes, programar sesiones con enlace de videollamada, subir materiales, responder dudas y contactar por WhatsApp. |
| **Administrador** | Dashboard y reportes, gestión de estudiantes y mentores (activar/desactivar), supervisión de mentorías, solicitudes y conexiones, programación de sesiones. |

Autenticación con **correo/contraseña** y **Google**, recuperación de contraseña y notificaciones dentro de la app.

## 🧰 Tecnologías

- **Frontend:** HTML5, CSS3 y JavaScript (módulos ES6), sin build ni dependencias.
- **Backend (BaaS):** [Firebase](https://firebase.google.com/) 10.12 — Authentication y Cloud Firestore.

## 📁 Estructura

```
.
├── index.html
├── app.js                 # Lógica de la app (vistas, autenticación, Firestore)
├── styles.css
├── firebase-config.js     # Configuración del proyecto Firebase
├── firestore.rules        # Reglas de seguridad de Firestore
├── avatars/               # Imágenes de perfil predefinidas
└── README.md
```

## 🚀 Ejecución local

> ⚠️ No abras `index.html` con doble clic: los módulos ES necesitan un servidor local.

```bash
git clone https://github.com/<tu-usuario>/<tu-repo>.git
cd <tu-repo>
npx serve
```

Abre <http://localhost:3000>.

## ⚙️ Configuración de Firebase

1. Crea un proyecto en la [consola de Firebase](https://console.firebase.google.com/).
2. Activa **Authentication** con los métodos *Correo/contraseña* y *Google*.
3. Crea la base de datos **Cloud Firestore**.
4. Registra una app web y copia su configuración en `firebase-config.js`.
5. Reemplaza `TU_CORREO_ADMIN@gmail.com` por el correo del administrador en `adminEmails` (`firebase-config.js`) y en la función `adminMail()` de `firestore.rules`. La cuenta admin debe tener el correo **verificado**.
6. Copia el contenido de `firestore.rules` en *Firestore → Reglas* y publícalo.
7. Si publicas la app en un dominio propio, agrégalo en *Authentication → Configuración → Dominios autorizados*.

> Las claves web de Firebase (`apiKey`, etc.) no son secretas: la seguridad real la dan las **reglas de Firestore** y los dominios autorizados.

## 🔐 Seguridad

Las reglas de `firestore.rules` aplican control por rol:

- Solo usuarios autenticados leen datos; los chats, mensajes y solicitudes solo los ven sus participantes o el administrador.
- El rol `admin` solo se puede crear con el correo de administrador verificado.
- Los usuarios no pueden cambiar su propio rol ni su estado `active`.
- Los materiales solo los publican mentores; las dudas, solo los estudiantes que las crean.

## 🗂️ Colecciones de Firestore

| Colección | Contenido |
|---|---|
| `users` | Perfiles de estudiantes, mentores y administradores (ID = UID de Auth) |
| `requests` | Solicitudes de mentoría y sus sesiones |
| `chats` / `messages` | Conversaciones y mensajes |
| `notifications` | Notificaciones dentro de la app |
| `ratings` | Calificaciones de estudiantes a mentores |
| `materials` | Materiales compartidos por mentores |
| `doubts` | Dudas de estudiantes y respuestas |

## 👥 Equipo

Completa aquí los nombres de los integrantes del proyecto.
