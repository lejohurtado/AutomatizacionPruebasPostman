# Automatización de Pruebas API REST - Postman
SI buscaron por todo lado una herramienta de automatización, también lo realice y mi conclusión la dejo a continuación.
Iré un poco mas rápido suponiendo que ya han utilizado la herramienta en un nivel básico.
## Trabajo con variables
Debemos primero tener claro el tema de las variables en Postman antes de adentrarnos a escribir **Script Tests** 
Postman nos ofrece la facilidad de trabajar con cinco tipo de variables:
 * Globales (Globals)
 * Colección (Collection)
 * Ambiente (Environment)
 * Datos (Data)
 * Locales (Local)

![enter image description here](https://assets.postman.com/postman-docs/var-scope.jpg)

Este es un ejemplo de como podemos invocar una variable de manera simple en postman: 

    {{VARIABLE}}
![enter image description here](https://assets.postman.com/postman-docs/vars-in-request.jpg)

Podemos configurar las variables a través de la UI de Postman en la vista rápida de variables
![enter image description here](https://assets.postman.com/postman-docs/env-quick-look.jpg)

Si queremos usarlas en los **Script Test** sera de la siguiente manera:
* Globals
	* `pm.globals.set("VARIABLE_KEY")`
	* `pm.globals.get("VARIABLE_KEY","VALUE")`
* Collection
	* `pm.collectionVariables.set("VARIABLE_KEY")`
	* `pm.collectionVariables.get("VARIABLE_KEY","VALUE")`
* Environment
	* `pm.environment.set("VARIABLE_KEY")`
	* `pm.environment.set("VARIABLE_KEY","VALUE")`
* Data
	* `pm.iterationData.get("VARIABLE_KEY")`
	* `pm.iterationData.set("VARIABLE_KEY","VALUE")`
* Local
	* `pm.variables.get("VARIABLE_KEY")`
	* `pm.variables.set("VARIABLE_KEY","VALUE")`

## Escribiendo Script Test en Postman
Hablemos donde y como escribir **Script** en Postman. Después de trabajar mucho tiempo con Postman se darían cuenta de las opciones **Pre-request Script** y **Tests** en las pestañas cuando armamos nuestra prueba a un servicio
![Pre-request Script](https://assets.postman.com/postman-docs/pre-request-tab-empty.jpg) 
![Tests](https://assets.postman.com/postman-docs/test-result-status.jpg)

* **Pre-request Script** es el código que se ejecutará ante que se envíe el request al servidor.
* **Tests** es el código que se ejecutara después que el servidor responda.
En ese orden de idea su ejecución se puede representar así.
![enter image description here](https://assets.postman.com/postman-docs/req-resp.png)
Postman entiende lenguaje Javascript el cual y la libreria de aserciones que usa es ChailJS con el cual podemos realizar BDD de una manera realmente simple.
Este seria su ejemplo mas básico para validar que la respuesta de llamada al servicio fue correcta

 ```JavaScript
	pm.test("Status test", function () {
		pm.response.to.have.status(200);
	});
```
