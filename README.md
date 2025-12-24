# 🎓 Gestión Académica (Frontend)

Este repositorio corresponde a la **parte frontend** de *Gestión Académica*, una aplicación web diseñada para llevar el **control académico completo de un instituto**, permitiendo la gestión de alumnos, asignaturas y calificaciones de forma centralizada y segura.

La aplicación está orientada a profesores y personal autorizado, ofreciendo una interfaz clara y moderna para consultar y administrar la información académica.

---

## 🧠 Descripción del proyecto

Gestión Académica es una **aplicación web de gestión educativa**.  
Este repositorio contiene exclusivamente el **frontend**, desarrollado con **Vue**, que se comunica con un **backend mediante una API REST** encargada de la lógica de negocio y el almacenamiento de datos.

El frontend se encarga de la visualización, navegación, validación básica y experiencia de usuario.

---

## ✨ Funcionalidades principales

- 🔐 Inicio de sesión para usuarios autorizados.
- 👨‍🎓 Gestión y visualización de alumnos.
- 📚 Gestión de asignaturas.
- 📝 Consulta y modificación de notas.
- 🧑‍🏫 Interfaz orientada al profesorado.
- 🧭 Navegación estructurada mediante rutas protegidas.
- 📊 Control académico centralizado.

---

## 🛠️ Tecnologías empleadas

- **Vue**: Framework principal para la construcción de la interfaz.
- **Vite**: Entorno de desarrollo.
- **JavaScript**: Lógica de la aplicación.
- **Vue Router**: Gestión de rutas y navegación.
- **Pinia**: Manejo del estado global (usuario, sesión y datos).
- **CSS**: Estilos personalizados de la aplicación.

---

## ⚙️ ¿Cómo funciona la aplicación?
1. El usuario accede a la aplicación web.
2. Se muestra una pantalla de inicio de sesión.
3. Al introducir credenciales válidas, el backend devuelve un token de autenticación.
4. El frontend guarda el estado del usuario mediante Pinia.
5. El usuario accede a las distintas vistas protegidas.
6. Cada vista consume la API REST para obtener o modificar información académica.
7. Si no existe sesión activa, el acceso a rutas privadas está bloqueado.


---

## 🔐 Login y seguridad
- El acceso a la aplicación requiere autenticación previa.
- El estado del usuario se gestiona mediante **Pinia**.
- Las rutas están protegidas mediante **guards de Vue Router**.
- Sin sesión activa, el usuario es redirigido al login.
- La validación de credenciales y permisos se realiza en el backend.
- El frontend actúa como capa de presentación y control de acceso visual.

---

## 🚀 Instalación y ejecución

Para ejecutar el proyecto en tu entorno local, asegúrate de tener **Node.js** instalado y ejecuta los siguientes comandos:

```sh
git clone https://github.com/Joositoo/Gestion-Academica-FRONT.git
cd Gestion-Academica-FRONT
npm install
npm run dev
```

La aplicación estará disponible en el navegador en:
```sh
http://localhost:5173
```

