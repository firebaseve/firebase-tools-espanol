# Firebase (CLI) en Español

#### Documentación de _firebase-tools_ en Español

---

Estas son las funcionalidades que ofrece la Línea de Comandos Firebase (CLI):

* Desplegar código y archivos estáticos de tus proyectos Firebase
* Ejecutar un servidor local para tu sitio en Firebase Hosting
* Interactuar con los datos de tu base de datos Firebase
* Importar/Exportar usuarios _a_ o _desde_ Firebase Auth

Para empezar a utilizar Firebase (CLI), puedes leer a continuación la lista completa de comandos o chequear la [documentación específica para el Hosting](https://firebase.google.com/docs/hosting/quickstart).


## Instalación

Para instalar Firebase CLI, primero necesitas [estar registrado en Firebase](https://firebase.google.com/).

Después necesitas instalar [Node.js](http://nodejs.org/) y [npm](https://npmjs.org/). Cabe destacar que instalar Node.js debe instalar npm también.

Una vez npm instalado, puedes obtener Firebase CLI con tan sólo ejecutar el siguiente comando:

```bash
npm install -g firebase-tools
```
Esto te va a permitir acceder de manera global al comando `firebase`.


## Comandos

**El comando `firebase --help` muestra la lista de comandos disponibles y `firebase <comando> --help` muestra los detalles de un comando individual.**

Si un comando es _específico a un proyecto_, debes estar dentro del directorio del proyecto con un alias activo de dicho proyecto o especificar la id del proyecto Firebase con `-P <project_id>`.

A continuación una breve lista de los comandos disponibles y sus funciones:

### Comandos Administrativos

Comando | Descripción
------- | -----------
**login** | Autentica tu cuenta Firebase. Requiere acceso al navegador web.
**logout** | Cierra la sesión actual de Firebase CLI.
**login:ci** | Genera un token de autenticación para uso en entornos no-interactivos.
**list** | Muestra una lista de todos tus proyectos Firebase.
**setup:web** | Muestra la configuración para el SDK Firebase JS.
**use** | Activa un proyecto Firebase; gestiona alias del proyecto.
**open** | Abre en el navegador recursos relevantes del proyecto.
**init** | Configura un nuevo proyecto Firebase en el directorio actual. Este comando creará un archivo de configuración `firebase.json` en dicho directorio.
**help** | Muestra información de ayuda sobre el CLI o comandos específicos.
