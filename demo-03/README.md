## Pasos de instalacion 

Ejecutar el siguiente comando ´´npm install´´

## Omitir archivos 
Se van a omitir estos archivos

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

## Eliminar 2do commit usando Mixed reset           git reset --hard d1b56fb
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



