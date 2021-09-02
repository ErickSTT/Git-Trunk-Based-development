# Git Trunk Based
> Una unica rama **master** de la cual parten los desarrolladores y crean ramas para sus caracteristicas, cuando su rama está completa y ha sido probada se envia un **MR (Merge Request)** a la rama principal (master).

![Flujo de trabajo](https://uploads.toptal.io/blog/image/129304/toptal-blog-image-1551794413174-f4139c4be533dc592d49f9a0bcc330f0.png)

1. Crear una rama de ciclo de vida corto partiendo del **master**
2. Realice los cambios aqui y haga los commits a esta rama. Se debe probar de manera exhaustiva localmente. 
3. Cuando este listo para hacer un merge, actualice su rama con los ultimos cambios de la rama **master**, para evitar conflictos y agilizar la integracion
4. Haga el **MR** de su rama a la **master**


# Tutorial
## Creando nuestra primera caracteristica 

1. Primero necesitamos clonar el repositorio 

	```
	git clone https://github.com/IndustryKcirePunk/trunk-based-development-example.git
	```
	> Por defecto, nos encontraremos en la `master`rama que actualmente solo tiene un archivo ```readme.md```. Comencemos a agregar algo de código.

2. Crea una nueva `new branch` partiendo de  `master`. Haga que el nombre de esta rama esté relacionado con el trabajo que se está realizando. Un ejemplo es colocar el nombre ```feature/7789``` con el numero de historia de usuario asignado.
	```git 
	git checkout -b feature/7789
	```
	**[Nota importante]** Estamos creando un `new branch`para asegurarnos de que `master`siempre esté en un estado desplegable. No queremos introducir cambios que potencialmente podrían romper el código en master. Siempre que queramos agregar una nueva característica a nuestro código base, se creará una nueva rama para desarrollar y probar dicha característica.

3. En nuestra nueva rama, creemos un archivo app.js de javascript que nos permita imprimir en consola ```Grupo STT es la mejor empresa```.  Agregamos y confirmamos el nuevo codigo.
	```javascript
	//app.js
	console.log('Grupo STT es la mejor empresa')
	```
	```git
	git add .
	git commit -m "Agregando mensaje en consola"
	```
4. Ahora mandemos nuestro codigo al repositorio.
	```git
	git push origin feature/7789
	```
	**[Nota importante]** Antes de que podamos fusionar nuestra nueva función a `master`, usted debe asegurarse de que su codigo funcione y ya pase las pruebas.
5. Ahora que hemos verificado que nuestra nueva caracteristica funciona, podemos crear un **PR (Pull Request)**

	 **[Nota importante]** En este momento el administrador de repositorio estara revisando su codigo, si cumple con todo los requisito de la historia de usuario el encargado hara un **MR (Mergue Request)**, y la rama ```feature/7789``` se eliminara automaticamente .
6. Una vez que revicen su **PR**, si necesitan un cambio, puede repetir los pasos **2 y 3**
7.  Y listo has cumplico los pasos del flujo de trabajo **git trunk based**, y tus cambios ya se encuentra en la rama ```master```

## Creando segunda caracteristica
Ya aprendimos el flujo de trabajo para trabajar en equipo con la metodologia **git trunk based development**, ahora que ¿Que pasa si otro compañero tambien le aprobaron el **PR**, y el master tiene nuevos campos y tu necesita trabajar en una nueva caracteristica?

1. Con este comando nos vamos a traer los ultimos cambios de la rama master
	```git
	git pull --rabase origin master
	```
	**[Nota importante]** Dado que nuestra **PR** sue aprobado y 	fusionado, debemos asegurarnos que nuestra rama , este actualizada
	 > **Nota** : Estamos usando la `--rebase`bandera para asegurarnos de que el historial de nuestro maestro local se alinee con el control remoto. ¡También previene los conflictos!
	
2. Ahora podemos crear una nueva rama para comenzar con la historia de usuario que se nos asignaron.

	```git
	git checkout -b feature/8890
	```
 
3. Ahora que nuestra rama local esta actualizada podemos comenzar creando nuestra rama, donde colocaremos la nueva caracteristica.		
	
	
	```javascript
	// app.js
	console.log('Grupo STT es la mejor empresa');
	console.log('Grupo STT is the best company');
	
	console.log('Grupo STT est la meilleure entreprise');
	```
	```git
	git add .
	git commit -m "Agregando mensaje en Frances
	```
4. Llevemos el codigo a el repositorio
	```git
	git push origin feature/8890
	```

## Primera version estable
Ya que hemos terminado nuestro proceso de todas las caracteristica requerida para una primera version estable, es hora de etiquetarla 

1. Aseguremonos que tengamos los ultimos cambios
	```git
	git checkout master
	git pull --rebase origin master
	git checkout -b Version/1.0
	git push origin Version/1.0
	```
	```git
	git tag -a m "Primera version para produccion 1.0
	git push origin --tags
	```


## Recomendaciones 
> Debes tener instalado Git Bash

Lo primero que debemos hacer es abrir nuestra terminal, pero con **git bash**, y ejecutamos el siguiente comando ```nano ~/.gitconfig```, y pegamos el siguiente codigo.

```git
[alias]
	b  = branch
	cm  = !git add -A && git commit
	ci  = commit -m
	co  = checkout
	cob  = checkout -b
	d  = diff
	l  = log
	lg  = log --pretty=format:'%h - %an, %ar : %s' --graph
	lgc  = log --graph --pretty=format:'%Cred%h%Creset -			%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)%Creset' --abbrev-commit --date=relative
	lgb  = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)%Creset' --abbrev-commit --date=relative --branches
	st  = status
	ri  = rebase --interactive
	rc  = rebase --continue
	mt  = mergetool
	rf  = reflog
	last  = log -1 HEAD
	alias  = config --get-regexp ^alias\\.
	lost  = fsck --full
	broken  = fsck --unreachable
	po  = push origin
	rs  = rebase --skip
	lgG1 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
	lgG2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
```

Impresionante, ahora te vas ahorrar varios segundo, y aumentar tu productividad.

## Mas atajos
Si ademas de eso, si pensaste que con eso ibas hacer mas rapido, que pasaria si te dijiera que se puede reducir mas aun, vamos a ponerlo en practica, vamos abrir el **```git bash```** de nuevo, y vamos a copiar y a pegar esos comando uno por uno:
```git
alias gb="git b"
alias gcm="git cm"
alias gci="git ci"
alias gco="git co"
alias gcob="git cob"
alias gd="git d"
alias gl="git l"
alias glg="git lg"
alias glgc="git lgc"
alias glgb="git lgb"
alias gst="git st"
alias gri="git ri"
alias grc="git rc"
alias gmt="git mt"
alias grf="git rf"
alias glast="git last"
alias galias="git alias"
alias glost="git lost"
alias gbroken="git broken"
alias gpo="git po"
alias grs="git rs"
```
Si te diste cuenta estamos haciendo un alias, de los alias que habiamos creados anterior mente, y con eso reducimos nuestro tiempo para trabajar con git
```
De git status pasamos a git st y de eso ahora tenemos gts
```
El ejemplo anterior no guarda permanentemente, los alias de consola, para hacerlo ejecute este comando **```nano ~/.bashrc```**, copia y pega todo lo anterior, guarda los cambios, y ejecuta esta comando para que se actualice la terminal y tenga la configuracion que le acabamos de poner **```source ~/.bashrc```**. Y listo, ahora tenemos mas productividad en el equipo.
