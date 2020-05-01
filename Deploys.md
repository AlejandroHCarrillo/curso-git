## Deployar en github

* Solo sirve para deployar contenido estatico
* Crear un proyecto enlazado al repositorio de github
* instalar el CLI de github
**npm install -g angular-cli-ghpages**

* Crear un deploy de produccion enlazado al url de github
**ng build --prod --base-href="https://[username].github.io/[repository]/"**

* **__Nota: terminar el url con diagonal__**

Para publicar del deploy hay que correr ngh y proporcionar las credenciales si son requeridas.

El alias corto para angular-cli-ghpages es **ngh**

Al terminar aparece el mensaje "Successfully published!"

Para automatizar este proceso se puede hacer en el archivo package.json
en:
>{ "scripts":{  
	"deploy:gh": "ng build --prod --base-href='https://[username].github.io/[repository]/' && ngh"  
  }  
}  

Para ejecutar este script usamos:
**npm run deploy:gh**

## Deployar en Firebase
Permite deployar contenido estatico, usar base de datos y provee servicios rest para su base de datos.

* Crear una cuenta en https://console.firebase.google.com
* Crear un proyecto nuevo 
* En la terminal bajar el CLI de las herramientas de firebase  
**npm install -g firebase-tools**

* Logearse para usar las heramientas, si continuas loggeado en la consola de google ya estas, pero si no, aparece un ventana del navegador pidiendo las credenciales.
firebase login

* Inicializar el proyecto 
firebase init

* Seleccionar la opcion que queremos Database, functions or hosting
* Seleccionar el proyecto donde queremos publicar

* En el proyecto creamos el archivo **firebase.json** para configurar 
>{  
  "hosting" : {  
	"public" : "dist",  
	"rewrites": [  
	  "source" : "**",  
	  "destination" : "/index.html"	  
	  ]   
  }  
}  

* Deployamos el proyecto para produccion:
**ng build --prod**

* Deployamos el proyecto a firebase
**firebase deploy**

Cuando nuestra aplicacion esta deployada nos muestra el URL donde podemos verla:  
**https://[proyecto].firebaseapp.com**

* La seccion rewrites sirve para redirigir las rutas a la ruta principal eso arregla el problema con los urls de una SPA.

Para automatizar este proceso se puede hacer en el archivo package.json
en:
> { "scripts":{  
	"deploy:firebase": "ng build --prod && firebase deploy"  
  }  
}

Para ejecutar este script usamos:  
**npm run deploy:firebase**


## Deployar en Heroku
* Descargar Heroku CLI de su pagina  
https://devcenter.heroku.com/articles/heroku-cli  
https://devcenter.heroku.com/articles/heroku-cli#download-and-install  

* Instalarlo
* Verificar la version 
**heroku --version**

* Loguearse en heroku usando correo y pasword de tu cuenta
**heroku login**

* Crear una aplicacion heroku, se debe poner un nombre unico o dejar que heroku elija uno por ti.
**heroku create [nombre unico opcional]**

* Al finalizar el comando mostrara la url de la aplicacion creada o abrirla usando:
**heroku open**

__**IMPORTANTES** Cambios al archivo package.json__

* Mover de "devDependencies" { } a "dependencies" {} las siguientes lineas
>"dependencies" {  
  "@angular/cli" : "x.x.x",  
  "@angular/compiler-cli" : "x.x.x",  
  "typescript" : "x.x.x"  
}

* Agregar esta linea a los scripts del package.json
>{   
  "scripts":{  
	  "postinstall": "ng build --prod"  
  }
}

Para iniciar el servidor node cambiar la seccion start de los scripts por:

>{  
  "scripts":{
	  "start" : "node server.js"  
	  "postinstall": "ng build --prod"  
  }  
}  

* Pasos pare deployar en heroku
**git add .**
**git commit -m "Preparacion para heroku"**
**git push heroku master**
**heroku open**

### Engines
Para establecer las versiones exactas para deployar hay que agregar a package.json

>{ 
  "scripts":{  
	"postinstall": "ng build --prod"  
  },  
...  
  "engines": {  
	"node": "x.x.x",  
	"npm": "x.x.x"  
  }  
}  

**Nota** para saber las versiones ejecutamos **__node --version__** y **__npm --version__** 






