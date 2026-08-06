# Despliegue del Sistema de Vacaciones CVM — GitHub + Firebase

## Requisitos previos

Instalar en tu computadora:

1. **Git**: https://git-scm.com/downloads
2. **Node.js**: https://nodejs.org (versión 18 o superior)
3. **Firebase CLI**: abrir terminal y ejecutar:
   ```
   npm install -g firebase-tools
   ```

---

## PASO 1: Crear proyecto en Firebase

1. Ir a https://console.firebase.google.com
2. Iniciar sesión con tu cuenta de Google (josdarwin2023@gmail.com)
3. Clic en **"Agregar proyecto"**
4. Nombre: `sistema-vacaciones-cvm`
5. Desactivar Google Analytics → **Crear proyecto**
6. Esperar a que se cree

### Activar Firestore (base de datos para que Caracas vea los datos)

1. En el menú lateral del proyecto, ir a **"Firestore Database"**
2. Clic en **"Crear base de datos"**
3. Seleccionar **"Modo de prueba"** (Start in test mode)
4. Ubicación: `us-central` o `southamerica-east1`
5. Clic en **"Habilitar"**

### Activar Hosting

1. En el menú lateral, ir a **"Hosting"**
2. Clic en **"Comenzar"** → Seguir los pasos (no ejecutar nada aún)

### Obtener la configuración de Firebase

1. En el menú lateral, ir a **"Configuración del proyecto"** (ícono de engranaje)
2. Bajar hasta **"Tus apps"** → Clic en el ícono **"Web"** (`</>`)
3. Nombre: `sistema-vacaciones` → **Registrar app**
4. Firebase te mostrará un bloque como este:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyB...",
  authDomain: "sistema-vacaciones-cvm.firebaseapp.com",
  projectId: "sistema-vacaciones-cvm",
  storageBucket: "sistema-vacaciones-cvm.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

5. **COPIAR esos valores**

---

## PASO 2: Configurar el proyecto

1. Descomprimir el ZIP `sistema-vacaciones-cvm.zip`
2. Abrir el archivo `public/index.html` con un editor de texto (Notepad++, VS Code, o el bloc de notas)
3. Buscar la sección que dice:

```javascript
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_PROYECTO.firebaseapp.com",
  projectId: "TU_PROYECTO",
  ...
```

4. **Reemplazar** los valores con los que copiaste de Firebase en el paso anterior
5. **Guardar** el archivo

---

## PASO 3: Crear repositorio en GitHub

1. Ir a https://github.com/new
2. Nombre: `sistema-vacaciones-cvm`
3. Marcar como **Privado** (tiene datos sensibles de trabajadores)
4. NO marcar ninguna casilla adicional
5. Clic en **"Create repository"**

---

## PASO 4: Subir a GitHub y desplegar

Abrir terminal/CMD en la carpeta del proyecto descomprimido y ejecutar estos comandos uno por uno:

```bash
cd sistema-vacaciones-cvm

git init
git add .
git commit -m "Sistema de Vacaciones CVM PIM III - versión inicial"
git branch -M main
git remote add origin https://github.com/josdarwin/sistema-vacaciones-cvm.git
git push -u origin main
```

Ahora desplegar en Firebase:

```bash
firebase login
firebase use --add
```
(Seleccionar tu proyecto `sistema-vacaciones-cvm`)

```bash
firebase deploy
```

Firebase te dará la URL:
```
https://sistema-vacaciones-cvm.web.app
```

---

## Cómo funciona la sincronización

- Cuando tú (PIM III) registras un reposo o una solicitud de vacaciones, **se guarda automáticamente en Firebase**
- Caracas (o cualquier persona con la URL) abre el sistema y **ve los datos en tiempo real**
- Si tú agregas un reposo, Caracas lo ve aparecer sin refrescar la página
- Las descargas de vacaciones, reposos e historial se generan en **formato Excel (.xlsx)**

---

## Actualizaciones futuras

Cada vez que modifiques el sistema:

```bash
git add .
git commit -m "Descripción del cambio"
git push
firebase deploy
```

---

## Notas importantes

- El repositorio debe ser **PRIVADO** en GitHub (datos de cédulas y nombres)
- Los datos base de vacaciones vencidas (1,220 registros) están embebidos en el HTML
- Las solicitudes, reposos y ediciones se sincronizan vía Firebase Firestore
- Las descargas se generan en Excel (.xlsx) con formato profesional
- Si Firebase no está configurado, el sistema sigue funcionando con localStorage (pero solo local)
