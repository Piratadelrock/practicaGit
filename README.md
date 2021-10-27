*PRACTICANDO GIT*
# README.md podemos buscar documentacion para el formato md (mark down)
# clonar un repositorio
	git clone <https://link-con-nombre-del-repositorio>
# iniciar un proyecto git 
	git init
# Ramas (branch): trabajo en paralelo en mismo proyecto simultaneamente 
 * crear rama
		git branch <nombre de rama>
		git checkout -b <nombre de la rama>
	* visualizar ramas 
		git branch
		git branch --list
	* cambiar de rama tambien para chequear archivos y commits
		git checkout <nombre rama>
		creando la rama, cambiamos a la nueva para programar las nuevas funciones
	* renombrar rama 
		git branch -m <nombre rama actual> <nombre rama nuevo>
		
	* Borrar una rama:
		git branch -d <nombre-de-la-rama>
		Sin embargo, puede que esta acción no nos funcione porque hayamos hecho cambios que no se hayan salvado en el repositorio remoto, o no se hayan fusionado con otras ramas. En el caso que queramos forzar el borrado de la rama, para eliminarla independientemente de si se ha hecho el push o el merge, tendrás que usar la opción "-D".
		git branch -D rama_a_borrar
	* mas info
		git branch -h
# El comando crea una rama local para enviar la rama a un repositorio remoto se usa
	git push <nombre-remoto> <nombre-rama>
 Hay algunos pasos que debes seguir para cambiarte exitosamente entre ramas:
 * Los cambios en tu rama actual tienen que ser confirmados 
   o almacenados en el guardado rápido (stash) antes de que cambies de rama.
 * La rama a la que te quieras cambiar debe existir en local.

# acceso directo que te permite crear y cambiarte a esa rama al mismo tiempo:

	git checkout -b <nombre-de-tu-rama>

# git status

# Añadir un único archivo:
	git add <archivo>
 * Añadir todo de una vez:
	git add -A
	git add .

# COMMIT 
 * CREAR COMMIT
	git commit -m "mensaje de confirmación"
 * AGREGAR AL COMMIT RECIENTE O ULTIMO CREADO 
	git commit --amend
  
# deshacer cambios tanto local como remoto se usara 
	* si esta modificado se puede deshacer cambios (sin hacer stage area) con: 
		git checkout -- <file>
	* si esta agregado (en el stage area) osea cuando damos add para un commit 
		git reset HEAD <file>
		-para eliminar la modificacion usamos el git checkout -- <file>
		
	* al realizar modificacion agregar con add y hacer commit 
	 cambio confirmado en el commit entonces podemos usar amend o usando reset
		git reset <hashcommit>
		git reset 423dfs2
		*asi volvemos al commit anterior o especificado y luego seguimos los pasos anteriores en caso de usar reset o checkout
	
	* elimina tanto del stage como los cambios locales
		git reset --hard <hashcommit>
		git reset --hard HEAD
	* elimina los commit y los deja en el stage
		git reset --soft <hashcommit>
		git reset --soft HEAD
	sirve para revertir un commit, descarta los cambios que se han hecho en un commit 
	* diff para comparar dos commits 
		git diff <hash1> <hash2>
		git diff HEAD~1	HEAD

	*CON ESTE CODIGO PODREMOS APUNTAR LOS COMITS y diferenciarlos de los commits anteriores al HEAD
	 git diff HEAD~1 HEAD
	DONDE EL 1 SIGNIFICA ANTERIOR, 1 COMMIT ANTERIOR 
	CAMBIANDOLO A 2, 2 COMMITS ANTERIORES, Luego usando para revertir el commit
			
		git revert HEAD
		git revert e64e7bb
		
		usando el log oneline tenemos el hash del commit y lo colocamos
		(presiona shift + q para salir)
	
	revertir sin hacer commit (REVIRTIENDO EL COMMIT DEL HEAD Y EL HEAD~1 OSEA EL ATERIOR)
		git revert --no-commit  HEAD
		git revert --no-commit  HEAD~1
	terminamos de hacer la reversion con:
		git revert --continue 
	dejando dos cambios revertido y es menos destructivo 


# despues de confirmar cambios y pasarlos al repositorio remoto 
	git push <nombre-remoto> <nombre-de-tu-rama>

  *	De todas formas, si tu rama ha sido creada recientemente, puede que tengas que 	cargar y subir tu rama con el siguiente comando:

	git push --set-upstream <nombre-remoto> <nombre-de-tu-rama>
or
	git push -u origin <nombre-de-tu-rama>

# obtener o recibir actualizaciones del repositorio 
	git pull <nombre-remoto>

# ver los commits registrados
	git log
  *ver los commits sin detalles 
	git log --oneline 
  *ver nombres de los punteros del repositorio
	git log --oneline --decorate
	ver en pantalla 
	git log --oneline | cat
	*parametro graph para mostrar los grafos  con los distintos commits hechos con nuestro proyecto, finalidad es mostrar una relacion con 
	el commit y la que los acompaña, por ejemplo un commit es el raiz cuando esta en el final, el siguiente seria el sucesor de la raiz, 
	el que le sigue seria el antecesor al sucesor del a raiz.
	git log --oneline --decorate --graph
	git log --online --all --graph

#fusionar ramas 
	se puede fusionar ramas una rama de origen y una rama de destino 
	por ejemplo una rama fix-fecha -> master 
		git merge <origen> <master>
	*esta actualizando mediante fast forward  tienes que hacer una fusion entre una rama que tiene modificaciones y no tiene modificaciones, seria mas facil mover el puntero a lo ultimo es decir el HEAD a la rama que se fusionado
		git merge <origen>  (y damos al enter)
	
	ES MUY IMPORTANTE QUE CUANDO PIDAN ALGUN CAMBIO ESTE SE HAGA DEPENDIENDO DE LA RAMA, ANALIZAR SI SIRVE CREARLA DESDE EL MASTER O EL MAIN Y ASI CREAMOS UNA RAMA A PARTIR DEL CAMBIO DESDE EL MASTER Y NO DESDE OTRAS IMPLEMENTACIONES

# completando el desarrollo en la rama y todo funciona correctamente pasamos a fusionar la rama con su rama padre (dev o master)
********************************
Primero, debes cambiarte a la rama dev:

git checkout dev

Antes de fusionar, debes actualizar tu rama dev local:

git fetch
Por último, puedes fusionar tu rama de características en la rama dev:

git merge <nombre-de-la-rama>

********************************

#CREANDO ALIAS PARA LOS COMANDOS 
	git config --global alias.(alias que queremos colocar)
	git config --global alias.lodag 'log --oneline --decorate --all --graph'
	
	git config --global alias.unstage 'reset HEAD --'
	
	PARA VER LOS ALIAS CREADOS 
		git config --global --get-regexp alias
	PARA ELIMINAR ALIAS
		git config --global --unset alias.lodag
	
	
# Ejecuta git remote add origin https://github.com/nombreDeUsuario/repositorio.git en la terminal. Aquí, nombreDeUsuario y  repositorio serán reemplazados por los valores proporcionados en el enlace copiado. Esto conectará la carpeta existente en tu sistema local al repositorio de Github recién creado.
	para continuar debemos agregar el comando 

    git push --set-upstream origin main

	en caso de que tengamos alguna falla usaremos el siguiente comando
		git pull origin master --allow-unrelated-histories
	
	git merge origin origin/master
	... add and commit here...
	git push origin master


Ejecuta git remote -v. Esto hace algo de magia usando git pull y git push para garantizar que el contenido de tu nuevo repositorio de Github y la carpeta en tu sistema local sean los mismos.

Finalmente, ejecuta git push origin master para empujar tus archivos a Github. Ten en cuenta que la última palabra en el comando master, no es una entrada fija cuando se ejecuta git push, puede ser reemplazada por cualquier “nombre_de_rama” relevante.

tratar:

git fetch origin master
git merge origin master
Después de escribir este código, recibí otro error: (no avance rápido)

Escribo este código:

git fetch origin master:tmp
git rebase tmp
git push origin HEAD:master
git branch -D tmp

	
# esto es para cuando tenemos errores con la conexion remota 
	git clone git@github.com:usuario/repo.git
	
	git init
   	git remote add origin git@github.com:alexhak1/ThinkSecWEB.git

	para hacer actualizar el repositorio
		git push origin master
	significa "hacer merge del local master la rama remota origin/master".
	

	git add --all
	git commit -am "primer commit local"

	git pull
o

	git push
o

	git push --set-upstream origin master
como el remoto tiene un commit que el local no tiene y viceversa No hay ancestro común y por lo tanto no se puede hacer merge.
Si el código del remoto es ligeramente parecido a tu código local y efectivamente quieres hacer un merge, la solución sería:

git fetch --all
git reset --soft origin/master
git add --all
git commit -am "comit encima del primer commit remoto"
git push origin master
Si de verdad los códigos no tienen nada que ver, puedes hacer:

git push -f --set-upstream origin master
Y con eso vas a pisar el remoto forzadamente con tus commits locales. Ojo que con esto se perderá lo que hay en el remoto.
