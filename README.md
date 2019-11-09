## Crear el repositorio				        
git init
## Creo el branch develop			        
git checkout -b develop
## Se agregaro el archivo bitacora al stage	
git add .
## se dio commit al archivo de bitacora		
git commit -m "Creacion de la bitacora"
## se subieron los cambios al branch develop	
## Se modifico el archivo de bitacora
## Se cambio el mensaje del ultimo commit		
git commit --amend -m "Creacion de la bitacora de trabajo"
## Se creo el branch master			        
git branch master
## Se modifico la bitacora en el branch Master
## Ver el log con formato                      
git log --oneline --decorate --all --graph 
## Crear alias para Log con formato            
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



