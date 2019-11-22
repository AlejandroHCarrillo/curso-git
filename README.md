# Guia de comandos de Git

## Clonar un repositorio en el directorio actual
git clone https://github.com/AlejandroHCarrillo/curso-git.git

## Clonar un repositorio en un direcrorio especifico
git clone https://github.com/AlejandroHCarrillo/curso-git.git

## Crear el repositorio				        
git init

## Creo el branch develop			        
git checkout -b develop

## Agregar el archivo bitacora al stage	
git add .

## Dar commit al archivo de bitacora		
git commit -m "Commit con mensaje"

git commit -am "Agrega todos los archivos al stage y hace el commit con mensaje"

## Cambiar el mensaje del ultimo commit		
git commit --amend -m "Amend cambia el mensaje del commit"

## Crear un branch 
git branch [nombre-del-branch]

## Crear alias para los comandos de Git, ver el log con formato
git log --oneline --decorate --all --graph 

## Crear alias para vel el Log con formato
git config --global alias.lg "log --oneline --decorate --all ## --graph"

## Usar el nuevo alias                    
git lg

## Crear alias status una linea con branch     
git config --global alias.s "status -s -b"

## Ver las diferencias del archivo original    
git diff / git diff --staged

## Para un archivo del stage                   
git reset HEAD [Archivo.ext]

## Para descartar los cambios de un archivo    
git checkout --[Archivo.ext]

## Commit 1 para probar Hard reset
git commit -am "Commit 1 para probar Hard reset"

## Commit 2 para probar Mixed reset
git commit -am "Commit 2 para probar mixed reset"

## Commit 3 para probar Soft reset
git commit -am "Commit 3 para probar soft reset"

La historia queda así
* a5d00b0 (HEAD -> develop) Commit 3 para probar soft reset
* ba88df5 Commit 2 para probar mixed reset
* 969c298 Commit 1 para probar Hard reset
* d1b56fb Comandos para resetear commits
*   055fd64 Merge branch 'master' into develop
|\
| * 3e5478f (master) Se modifico la bitacora en develop
|/
* 6bdff2c Agregando alias para status -s -b
* b87312e Agregando Alias al comando log en el branch develop
* 799bf46 Se creo el branch master
* 97bfaaa Agregar commandos Git a los pasos
* 4f80a76 Creacion de la bitacora de trabajo

## Eliminar 3er commit usando Soft reset            git reset --soft ba88df5

Se descarto el commit a5d00b0 quedando solo los comiits desde ba88df5 los archivos seguian ahi como WIP los cambios.
* ba88df5 Commit 2 para probar mixed reset
* 969c298 Commit 1 para probar Hard reset
* d1b56fb Comandos para resetear commits
* ...

## Eliminar 2do commit usando Mixed reset           git reset --mixed 969c298
Elimino el 2do commit, Quito del stage los archivos jpg y el archivo README.md pero los conservo en WIP

* 969c298 (HEAD -> develop) Commit 1 para probar Hard reset
* d1b56fb Comandos para resetear commits
* ...

## Eliminar 3er commit usando Hard reset           git reset --hard d1b56fb
Quito el archivo jpg que se habia agregado en el commit 2
Conservo como WIP los cambios en README.md el primer archivo jpg tambien esta en WIP

* d1b56fb (HEAD -> develop) Comandos para resetear commits
* ...

## Ver todos los movimientos de la historia aun cuando se hallan reseteado
git reflog

## Recuperando todos los commits perdidos 
git reset --hard a5d00b0
Se recuperaron todos los commits pedidos junto con los archivos
HEAD is now at a5d00b0 Commit 3 para probar soft reset

* a5d00b0 (HEAD -> develop) Commit 3 para probar soft reset
* ba88df5 Commit 2 para probar mixed reset
* 969c298 Commit 1 para probar Hard reset
* d1b56fb Comandos para resetear commits
* ...

## Comparar cambios entre 2 braches
git diff branch1 branch2

Para hacer un merge me tengo que poner sobre el branch que va atras, luego hacer el merge del branch que va adelante
En este caso Master esta atras de develop

    *   b1cb2c5 (develop) Merge branch 'master' into develop
    |\
    | * 947b0f7 (HEAD -> master, curso-git/master) Agregar el .gitignore
    | * b4b05e6 arreglando archivo README.md y bitacora.txt
    |/
    * 995de5d Commits eliminados y recuperados

## Nos cambiamos a Master
git checkout master

## Hacemos el merge de develop a master (en el cual estamos parados) SIN CONFLICTOS
git merge develop

## Eliminar branches
git branch -b [nombre-branch]

## Crear Tags
git tag [nombre-del-tag]
git tag -a v.1.1.0 -m "Version 1.1.0"

## Agregar un tag a un commit especifico (b4b05e6)
git tag -a v.0.0.1 [b4b05e6] -m "Version inicial"

## Eliminar Tag 
git tag -d [nombre-del-tag]

## Subir los tags al repositorio remoto
git push --tags

# Usar el STASH
## Ver el contenido del stash
git stash list

git stash list --stat       Muestra mas informacion de cada entrada del stash

gis show stash @[idStash]   Muestra el detalle de la estrada del estash

## Agregar el trabajo en proceso al stash
git stash 

git stash save

git stash save "Mensaje"    Guarda el trabajo en proceso con un mensaje descriptivo

## Recuperar el ultimo stash
git stash apply

## Recuparar un stash especifico
git stash apply [IdStash]

## Elimina una entrada del stash
Cuando hay conflictos no se elimina la entrada del stash, por lo que hay que hacelo manualmente
git stash drop 
git stash drop @[IdStash]

## Aplicar y limpiar el stash git stash apply + git stash drop
git stash pop 

## Limpiar stash
git stage clear

## Rebase
El rebase se usa para incorporar cambios de otro branch en nuestro branch de trabajo.
Si tenemos un branch de trabajo el cual se quedo atras algunos commits con respecto a master aplicamos un rebase. Esto incorpora los cambios a master antes de nuestro branch de trabajo y pone nuestros cambios despues de los cambios de master.

* Primero nos colocamos en nuestro branch de trabajo.

    git checkout [branchdetrabajo]

* Luego le aplicamos el rebase del branch que queremos incorporar a nuestro trabajo en este caso master 

    git rebase master

* Ahora nos movemos al branch master para incorporar los cambios contenidos en nuestro branch de trabajo

    git checkout master

* Incorporamos el branch de trabajo a master

    git merge [branchdetrabajo]

## Rebase - Squash
Squash se usa para unir 2 o mas commits en uno solo. Como cuando se hacen commits de correcciones se desean unir a un commit general sin mostrar los commits con las correcciones intermedias. Para obtener los utimos commits a partir de HEAD usamos ~ ejemlpo HEAD~4.

git rebase -i HEAD~4

Al usar el parametro -i indicamos que sea INTERACTIVO, lo cual nos abre un editor con los commits especificados en el HEAD, osea 4. Todos los commits tienen la palabra "pick", ademas muestra las siguientes opciones:

´´´
Rebase 7402030..cf4caf7 onto 7402030 (2 commands)

Commands:
p, pick = use commit
r, reword = use commit, but edit the commit message
e, edit = use commit, but stop for amending
s, squash = use commit, but meld into previous commit
f, fixup = like "squash", but discard this commit's log message
x, exec = run command (the rest of the line) using shell
d, drop = remove commit

These lines can be re-ordered; they are executed from top to bottom.

If you remove a line here THAT COMMIT WILL BE LOST.

However, if you remove everything, the rebase will be aborted.

Note that empty commits are commented out
´´´


# Enlazar a repositorio remoto
El repositorio de git puede ser enlazado a repositorios remotos en servidores publicos o privados que nos permiten mantener el codigo seguro en la nube.

https://git-scm.com/book/es/v1/Ramificaciones-en-Git-Ramas-Remotas

## Agregar el servidor remoto
git remote add origin https://github.com/AlejandroHCarrillo/curso-git.git

## Ver url repositorio remoto
git remote -v

curso-git       https://github.com/AlejandroHCarrillo/curso-git.git (fetch)
curso-git       https://github.com/AlejandroHCarrillo/curso-git.git (push)


## Uso del PUSH
Para subir los cambios al repositorio remoto es necesario hacer un push de la siguiente manera: 

git push -u origin master

* -u        Establece el branch por defecto para hacer push.
* origin    Es el nombre del repositorio
* master    es el branch que deseamos subir al repositorio remoto

[https://git-scm.com/book/es/v1/Git-en-un-servidor-Gitosis](https://git-scm.com/book/es/v1/Git-en-un-servidor-Gitosis)

## Git PULL
Git pull descarga los cambios del repositorio remoto e inmediatamente intenta hacer un merge **automaticamente**.

git pull

## Git FETCH
El git fetch descarga todos los cambios del repositorio remoto pero sin hacer el merge automatico.

git fetch

Despues de hacer el git fetch hay que hacer un git merge o un git pull para empatar los branches al head. Si hay conflictos hay que resolverlos localmente, despues hay que darle push para subir los cambios en el repositorio remoto.

_Es una buena practica hay que hacer un **fetch o un pul ANTES de subir los cambios**._


# Tutorial de Marckdown
[Markdown tutorial](https://www.markdowntutorial.com/)






## Referencias

[Tutorial GIT en español](https://git-scm.com/book/es/v1)

[Markdown tutorial](https://www.markdowntutorial.com/)

[markdown-cheatsheet-online.pdf](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)
