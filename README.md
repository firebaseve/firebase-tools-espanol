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

Agrega `--no-localhost` para iniciar sesión (por ejemplo: `firebase login --no-localhost`) copiando y pegando código en vez de utilizar la autenticación a través de tu navegador. Un caso de uso podría ser si te conectas a una _instancia_ mediante SSH, y necesitas autenticarte a Firebase en dicha máquina.

### Despliegue y Desarrollo Local

Estos comandos te permitirán desplegar e interactuar con tu sitio en Firebase Hosting.

Comando | Descripción
------- | -----------
**deploy** | Despliega tu proyecto Firebase. Depende de la configuración en `firebase.json` y el directorio local de tu proyecto.
**serve** | Inicia un servidor local con la configuración de tu Firebase Hosting. También depende de `firebase.json`.

### Comandos de Autenticación

Comando | Descripción
------- | -----------
**auth:import** | Importa lotes de perfiles hacia Firebase desde un archivo de datos.
**auth:export** | Exporta lotes de perfiles desde Firebase hacia un archivo de datos.

[Aquí](https://firebase.google.com/docs/cli/auth) puedes encontrar la documentación detallada.

### Comandos de Base de Datos

Comando | Descripción
------- | -----------
**database:get** | Trae datos desde la base de datos del proyecto actual y la muestra como JSON. Soporta _consultas_ en datos indexados.
**database:set** | Reemplaza todos datos en una locación especificada de la base de datos del proyecto actual. Toma como entrada un archivo, STDIN o un argumento de la línea de comandos.
**database:push** | Agrega nuevos datos a una lista en una locación especificada de la base de datos del proyecto actual. Toma como entrada un archivo, STDIN o un argumento de la línea de comandos.
**database:remove** | Borra todos datos en una locación especificada de la base de datos del proyecto actual.
**database:update** | Realiza una actualización parcial en una locación especificada de la base de datos del proyecto actual. Toma como entrada un archivo, STDIN o un argumento de la línea de comandos.
**database:profile** | Analiza el uso de la base de datos y genera un reporte.

### Comandos Cloud Firestore

Comando | Descripción
------- | -----------
**firestore:delete** | Borra _documentos_ o _colecciones_ de la base de datos del proyecto actual. Soporta borrado recursivo de _subcolecciones_.
**firestore:indexes** | Muestra todos los _indexs_ desplegados del proyecto actual.

### Comandos Cloud Functions

Comando | Descripción
------- | -----------
**functions:log** | Muestra los registros de las Cloud Functions desplegadas.
**functions:config:set** | Define _variables de entorno_ para el proyecto actual.
**functions:config:get** | Obtiene las _variables de entorno_ existentes en el proyecto actual.
**functions:config:unset** | Elimina las _variables de entorno_ definidas para proyecto actual.
**functions:config:clone** | Copia las _variables de entorno_ desde un proyecto hacia otro.
**experimental:functions:shell** | Emula localmente _Functions_ e inicia Node.js para que éstas puedan ser invocadas con datos de prueba.

### Comandos Hosting

Comando | Descripción
------- | -----------
**hosting:disable** | Deshabilita el tráfico web del proyecto activo en Firebase Hosting. El mensaje "Site Not Found" aparecerá en la URL de tu proyecto luego de ejecutar este comando.

## Uso con Sistemas CI

Firebase CLI requiere de un navegador web para completar el proceso de autenticación, sin embargo es totalmente compatible con CI y otros entornos sin interfaz gráfica.

1. En una máquina con navegador web, instala Firebase CLI.
2. Ejecuta en la terminal `firebase login:ci` para autenticarte y mostrar un nuevo token de acceso (la sesión actual no se verá afectada).
3. Guarda el token de acceso en un lugar seguro pero accesible en tu sistema CI.

Existen dos maneras de utilizar este token al ejecutar comandos Firebase:

1. Guarda el token como una variable de entorno llamada `FIREBASE_TOKEN` y automáticamente será utilizado.
2. Ejecuta todos los comandos en tu sistema CI con la `bandera` `--token <token>`.

El orden de procedencia para cargar el token es `bandera`, variable de entorno, proyecto actual.

En cualquier máquina con Firebase CLI, ejecutar `firebase logout --token <token>` revocará de inmediato el acceso al token especificado.

## Uso como Módulo

Firebase CLI puede ser también utilizado programáticamente como un módulo Node estándar. Esto sólamente puede ser logrado en tu máquina pero no en las Cloud Functions. Cada comando es expuesto como una función que toma Objectos como opciones y retorna Promesas. Por ejemplo:

```js
const client = require('firebase-tools');

client.list()
  .then(data => console.log(data))
  .catch(err => {
    // haz algo con el error.
  });

client.deploy({
  project: 'myfirebase',
  token: process.env.FIREBASE_TOKEN,
  cwd: '/path/to/project/folder'
}).then(() => {
  console.log('Rules have been deployed!');
}).catch(err => {
  // haz algo con el error.
});
```
