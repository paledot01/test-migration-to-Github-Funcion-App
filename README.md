## Creando Workflow para el Funcion APP modo NOOB - Autenticacion Básica :
Al crear una instancia de un Funcion App en Azure Portal, te da la opcion de implementar el deploy automatico, este opcion crea un workflow en tu proyecto y agrega un secret en tu proyecto como "Repository Secret".
1. Para crearlo manualmente, solo necesitas crear el workflow que es un archivo YML dentro de la carpeta `.github/workflows` en la raiz del repo y ahora vas a tu *Funcion App < Overview < Get publish profile* descargas el archivo dentro hay un XML que funciona como tu autorizacion para deployar al Funcion App, copias todo el contenido y lo guardas como un secrete dentro de tu repositorio.
2. Recuerda que si tu **secret** esta dentro de un entorno entonces se debe especificar el entorno antes de usar el secret en el workflow.

template del workflow: Azure Portal automatico

## Creando Workflow para el Funcion App, modo GOOD - Autenticacion con Entra ID :
1. Crea el workflow manualmente en la carpeta `.github/workflows`, en la raiz del repo.
2. La plantilla esta basada en el ejemplo proporcionado por Azure de la siguiente documentacion: [Continuous delivery by using GitHub Actions](https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-github-actions?tabs=linux%2Cjavascript&pivots=method-manual)
3. Para que el workflow se autentique de una manera mas segura y pueda deployar al Funcion App, agregaremos a la plantilla un login y logout a Azure, para esto necesitaremos un **secret** en el workflow con la credenciales.
4. Las Credenciales son las siguientes:

```json
{
  "clientId": "XXXXXXXXXXXXXXXXXX",
  "clientSecret": "XXXXXXXXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXXXXXXXXXXXX",
  "tenantId": "XXXXXXXXXXXXXXXXXX"
}
```
5. Todos estos valores los encontrarás dentro del App Registration del Function App, si aun no esta registrado la aplicación tendras que hacerlo.
6. Si no puedes acceder al `clientSecret` entonces podras crear uno nuevo en *Tu_App_Registration < Manage < Certificates & secrets < New client secret*. Apunta el nuevo *secret* antes de salir de la página.
7. Con todos los valores, creamos el secret dentro de tu repositorio, con el mismo nombre usado en el workflow.
   
template del workflow: [Actions Workflow Samples - Azure](https://github.com/Azure/actions-workflow-samples/blob/master/FunctionApp/linux-node.js-functionapp-on-azure.yml)
