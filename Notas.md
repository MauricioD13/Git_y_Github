# Git y GitHub

## Sistema de control de versiones

- git init: Se inicia el repositorio en la carpeta en la que se este haciendo el proceso, en este repositorio se guardaran los cambios de los archivos
- git add [archivo]: Se agrega el archivo en cuestion
- git commit:  Envia los ultimos cambios de archivo a la base de datos del sistema de control de versiones
- git commit -m "Mensaje de la version"
- git add . → Agrega todos los archivos que hayan cambiando en la carpeta actual
- git status : Status de la base de datos, si se ha hecho un cambio y no se ha guardado alli aparecerá
- git show: Muestra cambios historicos hechos y quienes lo hicieron
- git log [archivo] : historia entera de un archivo
- git push: Enviar a un repositorio remoto los cambios hechos en un archivo
- git rm [archivo]: Remover un archivo

## Staging y los repositorios: Ciclo básico de trabajo en Git

git init : 

Se crea el staging que es un espacio de memoria RAM donde se agregan lo cambios hechos al archivo y se crea el repositorio que es una carpeta .git . 

El archivo que esta en la carpeta en donde se inicio el repositorio pero no se ha realizado el comando git add, entonces el archivo esta en un estado no rastreado o untracked

git add :

El archivo pasa al area de staging donde esta esperando a ser enviado al repositorio. Staging es el estado temporal donde se editan los archivos, un area de preparación.

Cuando se realiza este comando el archivo ahora esta rastreado o tracked → Parte de staging. Es sistema git esta revisando si hubo cambios en archivo, si los hubo entonces se pasan a staging en el momento de realizar el git add

git commit 

El archivo se va al repositorio, el nombre de este repositorio por defecto es master donde van a estar todos los cambios del archivo.

Los cambios pasan de estar trackeados en el staging a estar trackeados en el repositorio. 

Cada vez se realiza un commit es una nueva version del archivo y el numero que tiene cada commit es el nombre interno en la base de datos de git 

git checkout

Traer los ultimos cambios guardados en el repositorio al archivo que esta en mi carpeta local 

Dependiendo de las modificaciones del comando checkout es posible traer alguna version anterior o solo algunos cambios etc...

## Branch y Merge en Git

Por defecto se inicia en la rama Master, en esta rama se pueden crear muchos commits es decir muchas versiones hasta la actual

- De alguna de las versiones hechas por el commit se puede crear una rama diferente que sea experimental o development para probar diferentes cosas.
- Por otro lado, se puede hacer otro tipo de rama que en la industria se llama hotfix, esto sucede cuando hay un bug en la rama principal, si posteriormente se quiere llevar el codigo que esta en esta rama a la rama principal es necesario hacer un MERGE
- Version head → Version actual
- Un merge se puede hacer también con una rama experimental o development
- Nota: Es posible que al momento de hacer un merge algunos archivos entre en conflicto lo que hace que el código se rompa

## Repositorio en Git y Primer commit

Cambios atómicos → Cada cambio se guarda de una manera independiente

Crear archivo .txt en la carpeta donde se inicio el repositorio

- git rm —cached [archivo]: Este comando remueve la archivo en cuestion de la memoria RAM (staging)
- git config —list : Configuracion por defecto de git
- git config —list —show-origin: en que lugar estan guardadas la configuraciones
- git config —global [user.name](http://user.name) "[Nombre]"
- git config —global [user.email](http://user.email) "[Correo]"
- git add: Siempre que se hagan cambios a un repos debe hacerse un git add

## Analizar cambios en los archivos de tu proyecto en Git

- git show [archivo] : cambios a un archivo

    ![Alt text](/Imagenes/Untitled.png)

    git hace un diff con la version a y b que tiene en la base de datos para poder mostrar las diferencias entre versiones

    @@ -1.4 +1,6 @@ → Indica cuantos bytes cambiaron

     git muestra los cambios actuales en verde y lo que se cambio en rojo, si no tiene color entonces no fue modificada esa parte

- git log [archivo] : muestra la historia de los commits

    ![Alt text](/Imagenes/Untitled 1.png)

- git diff [commitA] [commitB]: Este comando compara las diferencias entre dos versiones en la base de datos

    Para poder usar este comando correctamente se toman los codigos que aparecen despues del commit cuando se usa el comando git log

    0a4e6ab4533cd86d7cc8cb366dc7c81120940b48 → version actual (head): commitA

    7c2a930491879210ac146a07af6b0e357a28d767 → primera version: commitB

    ![Alt text](/Imagenes/Untitled 2.png)

    Dependiendo del orden en que se pongan los codigos git interpretará cosas diferentes

    Para que sea mas intelegible es buena practica poner primero la version mas antigua y despues la versión mas actual

## Volver en el tiempo en nuestro repositorio utilizando reset y checkout

- git reset [codigo]: Este comando se usa para devolver a alguna version anterior del archivo, solo hay que poner el codigo del commit al que se quiere devolver
    - git reset [codigo] — hard: Se devuelve absolutamente todo a esa version (mas comun)
    - git reset [codigo] — soft: Se devuelve a la version requerida pero los cambios que estan en staging siguen ahí
- git diff → Este comando sin ningun codigo, compara los cambios que estan en el staging con el archivo actual
- git log —stat → Muestra los cambios especificos a cada archivo
- git checkout [codigo del commit] [archivo]→ Retorna la version requerida del archivo en cuestion
- git checkout master [archivo] → Retorna la version actual del archivo
- git

## Git Reset vs Git rm

- git rm : Este comando nos ayuda a eliminar archivos de Git sin eliminar su historial del sistema de versiones. Esto quiere decir que si necesitamos recuperar el archivo solo debemos “viajar en el tiempo” y recuperar el último commit antes de borrar el archivo en cuestión.

    Para poder usar el comando se debe poner una de estas dos banderas:

    - git rm --cached: Elimina los archivos del área de Staging y del próximo commit pero los mantiene en nuestro disco duro.
    - git rm --force: Elimina los archivos de Git y del disco duro. Git siempre guarda todo, por lo que podemos acceder al registro de la existencia de los archivos, de modo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).
- git reset:

Hay dos formas de usar `git reset`: con el argumento `--hard`, borrando toda la información que tengamos en el área de staging (y
perdiendo todo para siempre). O, un poco más seguro, con el argumento `--soft`, que mantiene allí los archivos del área de staging para que podamos
aplicar nuestros últimos cambios pero desde un commit anterior.

- `git reset --soft`: Borramos todo el historial y los
registros de Git pero guardamos los cambios que tengamos en Staging, así podemos aplicar las últimas actualizaciones a un nuevo commit.
- `git reset --hard`: Borra todo. Todo todito, absolutamente todo. Toda la información de los commits y del área de staging se borra del historial.
- `git reset HEAD`: : Este es el comando para sacar archivos del área de Staging. No para borrarlos ni nada de eso, solo para que los últimos cambios de estos archivos no se envíen al último commit, a menos que cambiemos de opinión y los incluyamos de nuevo en staging con git add, por supuesto.

## Flujo de trabajo básico con un repositorio remoto

### Flujo de trabajo normal:

![Alt text](/Imagenes/Untitled_3.png)

![Alt text](/Imagenes/Untitled_4.png)

![Alt text](/Imagenes/Untitled_5.png)

### Flujo de trabajo remoto:

El equivalente de git init pero para un repositorio remoto

![Alt text](/Imagenes/Untitled_6.png)

![Alt text](/Imagenes/Untitled_7.png)

- git push: Ultima version de los commits se envie al repositorio remoto
- git fetch: Trae cambios hechos en el repositorio local al repositorio remoto
- git merge: Funsiona la ultima version del repositorio local con la version del repositorio remoto
- git pull: Fusiona el concepto de fetch y merge

![Alt text](/Imagenes/Untitled_8.png)

![Alt text](/Imagenes/Untitled_9.png)

## Introducción a las ramas o branches de Git

Rama principal → Master

- git branch <nueva rama> : Comando para crear una nueva rama
- git checkout -b <rama> : Este comando cambia a la rama especificada, es decir, cambia el HEAD, este cambia al ultimo commit de la rama especificada. En general este comando sirve para ir al commit que se necesite.
- git commit -am <comentario>: Este comando es un git add y un git commit juntos

    Notas: Los cambios que aparecen en el archivo que se esta trabajando dependen de la rama en la que se esta trabajando, estos cambios  seran los del ultimo commit de la rama en cuestion 

- Si se usa el comando git show cuando se esta en  la rama nueva entonces es posible ver donde se creo esta nueva rama, es decir , en donde fue el ultimo commit del master

![Alt text](/Imagenes/Untitled_10.png)

## Fusion de ramas con git merge:

Cambiar cabera y agregar contenido al master

Cuando se hace un merge la rama secundaria se une al master, es decir , que es el final de la rama secundaria.

git merge <rama>:

- Cuando se va a realizar un mergegit  se debe hacer en la rama en la que se quiere seguir, generalmente se hace un merge estando en el master, es decir, se le hace un merge a la rama secundaria desde la rama master
- Si al momento de hacer un merge alguna parte del codigo fue editada en las dos ramas por la misma persona entonces se dispara una alerta de conflicto
- Cuando se hacer el merge se crea un commit definitivo de la fusion de las dos ramas

## Resolución de conflictos al hacer un merge

Cuando dos programadores hacen cambios en las mismas lineas de codigo entonces git manda alertas al momento de hacer un merge para decidir cual de las lineas de codigo seran las que se usarán

![Alt text](/Imagenes/Untitled_11.png)

Si hay un conflicto git pone los signos <<<<< HEAD que es hacia donde se hizo el merge y luego los signos >>>> <rama> que es la rama con la que se hizo el merge. Si no se esta en un editor de codigo con las funciones de git entonces solo hay que quitar estos simbolos y dejar el codigo que sea conveniente.

Por otro lado Visual Studio Code tiene la opcion de aceptar los cambios directamente en el editor dandole click a la opcion que sea mas conveniente

![Alt text](/Imagenes/Untitled%2012.png)

## Uso de GitHub

Es un sitio web con un super servidor de git donde cualquiera puede clonar un repositorio donde las personas pueden interactuar

Despues de iniciar sesion:

- Crear repositorio y inicializar archivo README
- RAW: Mirar el archivo en texto plano
- Blame: De quien es la culpa del lo que le sucede al archivo
- History: Muestra el historial de ese archivo

Para subir codigo a nuestro repositorio:

- Code → Copiar url que dice ahi ( de HTTPS)
- Ubicarse en la carpeta correspondiente
- git remote add origin <URL> :Agregar a git un origen remoto de nuestros archivos
- git remote -v : Muestra el origen para hacer fetch y un push
- git push origin master: Este comando le indica a git que envie al origen, que es la url de github, la rama master → Error se deben integrar los cambios remotos
- git pull origin master: hacemos un pull del origen hacia nuestra rama master
- git pull origin master —allow-unrelated-histories : permite que se fusiones historias no relacionadas, es decir, donde los proyectos no tienen commits comunes, solo cuando se inicia el repos
- 

## Llaves publicas y privadas

Cifrar el mensaje con un contraseña → Cifrado simetrico → El problema es el envio de la llave

Cifrado asimetrico → Llave publica y privada

- Envio la llave publica → Llave publica que sirve para cifrar el mensaje
- Solo la llave privada sirve para descifrar el mensaje

## Configurar tus llaves SSH en local

Una de las formas para acceder al repositorio remoto es como se hizo anteriormente por HTTPS que aunque esta encriptado en el camino, es posible que si alguien accede al pc pueda tomar las credenciales del repositorio. Ademas hay que poner las credenciales cada vez que se haga un push.

Para solucionar este problema se usa el protocolo SSH (Secure Shell) con el uso de llaves publicas y privadas.

- En local se crea una llave publica y privada, se envia la llave publica a github
- Se cirfra la llave publica de github con mi llave publica
- Ahora se puede hacer una conexion en los dos sentidos de manera segura

Para configurar las llaves:

- Ir al directorio home
- Cambiar la configuracion de git → Agregar correo que se tiene en github
    - Agregar correo que se tiene en github
    - git config —global [user.email](http://user.email) "<email>"

Crea las llaves:

- En git bash:
    - ssh-keygen -t rsa -b 4096 -C "<email>" : -t para el arlgoritmo que se usara, -b para la complejidad matematica, y -C para el correo con el que se relacionaran las llaves
    - Luego se elije una carpeta donde guardar las llaves, es recomendable solo dar enter y dejar que el sistema las acomode en el home
    - Contraseña adicional (opcional)

    Revisar que el servicio de llaves ssh este activado

    - eval $(ssh-agent -s): Si este comando da un PID entonces esta funcionando el programa

    Luego se debe agregar la llave al sistema:

    - ssh-add ~/.ssh/id_rsa → Se agrega la llave privada al sistema, la ruta especificada depende de donde se genero la llave

## Conexión a GitHub con SSH

- En github:
    - Settings →SSH and GPG keys → New SSH key
    - Luego se copia la llave publica y se pega en github
    - Posteriormente al momento de obtener la url del repos en lugar de copiar la url HTTPS se dan click en "use ssh" y se copia la url SSH.

    Luego se cambia la url del origen del repositorio:

    - git remote set-url origin <url ssh>
    - git remote -v : para verificar

    Antes de hacer un commits se debe traer la ultima version que se tiene en el repositorio remoto

## Tags y versiones en Git y Github

Los proyectos de codigo abierto tiene versiones o releases, cuando se decide que se envia el codigo que al parecer ya esta listo.

- git log: se pueden ver la historia
- git log —graph : se puede ver graficamente como esta la historia
- git log —graph —decorate —oneline: sirve para mirar de manera grafica pero mas comprimida la historia del repo

Tags:

Agregar un tag:

- git tag -a v0.1 -m "Resultado de las primeras clases del curso" <hash del commit> : Se debe especificar a que commit se le quiere agregar el tag
- git tag : Devuelve los tags que se han puesto
- git show-ref  —tags : Mostrar a que commit esta anclado un tag
- git pull origin master: antes de hacer algun cambio para que no haya conflictos
- git push origin —tags: con este comando se empujan a github todos los tags que se crearon

Borrar un tags:

- git tag -d <nombre del tag> : para eliminar (delete) un tag
- git push origin :refs/tags/<nombre del tag> : Dando que los tags tienden a quedar en el repos remoto hay que utilizar este comando para poder quitar los tags de github

Crear un alia

- git config —global aliar.<nombre del alias> "<comando de git para hacer el alias": Este comando funciona para configurar un alias a un comando muy largo
- Ej:

```bash
git config --global alias.tree "log --graph --decorate --oneline"
```

## Manejo de ramas en Github:

- git show-branch: Comando que muestra las ramas que existen y sus historias
- git show-branch —all: Muestra mas informacion que el comando anterior
- gitk : comando que despliega otra ventana donde se pueden ver los cambios de manera mas visual

Para enviar una rama a github hay que ubicarse en al rama respectiva y realizar un push de esa rama:

- git checkout <rama>
- git push origin <rama>

Nota: Siempre se deben traer primero los ultimos cambios que hubo en el repos remoto

## Configuracion multiples colaboradores en un repositorio en GitHub

Para poder agregar a un colaborador al repositorio, hay que ir a los settings del repositorio y hacer lo siguiente:

- Manage access → Invite a collaborator → <usuario de github para agregar>
- Es necesario saber el nombre de usuario de la persona que va a colaborar para poderla agregar

Antes de este proceso la persona puede clonar el repos y hacer git pull pero no puede hacer push 

- Luego de enviar la invitacion la persona debe hacer la invitacion que llego a su correo y ya puede hacer push al repos

## Flujo de trabajo profesional: Haciendo merge de ramas de desarrollo a master

Mejores practicas dicen que los archivos binarios deberian estar aparte, no se deberian agregar al repositorio.

Si por alguna razon se envian los binarios al repo entonces consumira mucho mas espacio que el texto plano normal

Si ese binario se cambia en local y se envia al repo remoto, este se demorar en hacer los cambios porque tiene un cache intermedio para cargar los cambios de la imagen

Importante: Cuando se tenga listo un trabajo en una rama de desarrollo, como empleado, hay que enviar el trabajo a la rama de desarrollo respectiva

El jefe o la persona correpondiente sera la encargada de fusionar las ramas despues de que se le haya hecho la revision final 

No se deben hacer commits al master en un entorno de trabajo profesional, los commits al master los debe hacer la persona encarga 

## Flujo de trabajo profesional con Pull requests

En un entorno profesional se bloquea el master para que haya un code review

Prueba que se parezca al entorno de producción, se parece lo mas posible.

Pull requets: Estado intermedio entre antes de enviar el merge → Característica de github

- merge request
- push request

![Alt text](/Imagenes/Untitled_13.png)

## Utilizando Pull Requests en GitHub

Es buena practica, crear una rama para realizar correcciones a el proyecto

Pull request:

- New pull request
- Abre un pestaña donde se puede configurar el pull request
- Se pueden agregar colaboradores, etiquetas, asignaciones, etc...
- Create pull request

Pull request:

Es una funcionalidad de github (en gitlab llamada merge request y en
bitbucket push request), en la que un colaborador pide que revisen sus
cambios antes de hacer merge a una rama, normalmente master.

Al hacer un pull request se genera una conversación que pueden seguir los demás usuarios del repositorio, así como autorizar y rechazar los
cambios.

El flujo del pull request es el siguiente

1. Se trabaja en una **rama paralela** los cambios que se desean (`git checkout -b <rama>`)
2. Se hace un **commit** a la rama (`git commit -am '<Comentario>'`)
3. Se **suben** al **remoto** los **cambios** (`git push origin <rama>`)
4. En GitHub se hace el `pull request` comparando la **rama master** con la rama del **fix**.
5. Uno, o varios colaboradores revisan que el **código sea correcto** y dan **feedback** (en el chat del pull request)
6. El colaborador hace los cambios que desea en la **rama** y lo **vuelve a subir** al remoto (automáticamente jala la historia de los cambios que se hagan en la rama, en remoto)
7. Se **aceptan los cambios** en GitHub
8. Se hace **merge** a `master` desde GitHub

**Importante**: Cuando se modifica una `rama`, también se modifica el `pull request`

**Nota**: Cuando se ponen reviewrs es necesario que ellos aprueben el cambio para poder hacer el merge

- Cuando se hace un merge del pull request, github da la opcion de borrar el branch para limpiar la ramas que no se necesitan, los commits hecho en esta rama quedaran como hecho en el master

Pull request → permite trabajar en staging del lado del servidor 

## Creando un Fork, contribuyendo a un repositorio

Cuando una persona no es colaboradora de un repositorio en github, existe la posibilidad de hacer un fork al repos 

- Un fork es hacerle una copia al proyecto para que quede como repos de la otra persona que no es colaboradora
- Si yo hago un fork a un proyecto que no me pertence, se crea una copia del repos que sera mia. Este nuevo repos que es mio lo puedo utilizar de la manera que quiera con github y git. Si por alguna razón quiero colaborar a un codigo open source entonces debo hacer:
    - Despues de hacer lo cambios que quiero al proyecto y estan en github en mi repos hago un pull request

        → New pull request → Esta la posibilidad de comparar los cambios entre forks 

        → Tambien se puede hacer comparacion y pull request de una rama del repo

        → Create pull request → Mensaje de contribucion 

- La persona que es dueña del repos original ve los cambios para hacer merge, github muestra los cambios cuando se ve el pull request. Si ha esta persona le gusta entonces aceptara el pull request

Si ya hice un fork de un repo y la persona dueña del repo original hace commits posterior a mi fork entonces tendre un proyecto que esta desactualizado con respecto al repo original.

GitHub nos dice cuantos commits hay de diferencia entre mi head master del head master de el repo original.

- Para solucionar esto se puede hacer un pull request del repo original al repo clonado
- La otra opcion crear un nuevo remoto en git del proyecto original para actualizarlo en local
    - git remote add <nombre> <url>
    - Lo usual es que se llame upstream: git remote add upstream <url>
    - git pull upstream master
    - git push origin master

![Alt text](/Imagenes/Untitled_14.png)

## Haciendo deployment a un servidor

Despues de configurar un servidor ya sea apache o nginx, se clona el repo en el servidor para poder obtener los archivos a lo que se les quiere hacer deploy

- Si se actualiza el codigo en github se debe hacer un git pull para traerse los ultimos cambios al servidor
- Tener el directorio .git visible y desprotegido no es una buena practica puesto que alguien desconocido puede acceder a ese directorio
- Existe software especializado en deploy tal como Travis CI o Jenkins

## Ignorar archivos en el repositorio con .gitignore

Dado que hay archivos que no deben ser agregados al repositorio por motivos de seguridad git tiene el archivo .gitignore para solucionar este problema.

- Se crea un archivo de nombre .gitignore donde se podran los nombre de los archivos que se quieren ignorar
    - Si se quiere ignorar todos los archivos jpg entonces se escribe → *.jpg
    - Si se quieren generar excepciones sobre lo que ya se ignoró entonces se usa el simbolo → !
    - Este archivo .gitignore es el que se agrega al repos con git add y luego un commit

## [Readme.md](http://readme.md) es excelente práctica

.md siginifica que el readme estara en un lenguaje llamado mark down que es un intermedio entre el texto plano y HTML

Para poder usar .md se aconseja usar paginas que ayuden en la redaccion de este tipo de archivos como: 

- [https://pandao.github.io/editor.md/en.html](https://pandao.github.io/editor.md/en.html)

## Tu sitio web público con GitHub Pages

Hosting gratis de github pages

[pages.github.com](http://pages.github.com) → Sitio autoexplicativo 

- Crear un repositorio con mi nombre de usuario
- Luego clonar el repos en local
- Crear un archivo que se llame index.html
- Hacer push al repos remoto
- Settings → github pages → master branch
- <nombre de usuario>.github.io

Para que cargue mi html en la raiz el nombre del repo debe ser el siguiente :

- <nombre de usuario>-github.io

## Git Rebase: reorganizando el trabajo realizado

git rebase → Reescribe la historia del repositorio, cambia la historia de donde comenzo la rama y solo debe ser usado de manera local

- Si se tiene una rama y por alguna razon se quiere que esos commits de la rama se vuelvan commits en la rama principal entonces se debe usar el comando rebase

**Nota**: Es muy mala práctica usar rebase en repositorio remoto, la historia del repositorio remoto debe estar intacta

- git rebase master → Este comando se ejecuta en la rama secudaria. La rama secundaria se va a pegar a la rama master.
- Si en la rama master se hizo un commit despues de hacer la creacion de la rama y posteriormente se hace un rebase a la rama secundaria entonces es como si la rama secundaria se actualizar con el ultimo commits de la rama master

**Nota:** Se debe hacer primero un rebase en la rama secundaria o la rama que cambia y luego un rebase a la rama final. Si no se cumple este orden se entra en un conflicto que se soluciona con un git reset

## Git Stash: Guardar cambios en memoria y recuperarlos después

git stash es un comando que devuelve el archivo o el repos al ultimo commits que se hizo en caso de que se haya guardado un archivo o se necesite probar cambios pequeños.

- Cuando se ejecuta el stash los cambios se guardan en memoria pero no estan en el archivo ni son un commit
- git stash save "mensaje" : mandar al stash los cambios del archivo con un mensaje
- git stash pop : Recupera los cambios del stash a mi zona de staging
- git stash list → Muestra los elementos que estan en el stash
- git stash branch <rama> : Si por alguna razon se necesita una rama para los cambios que estan en el stash este comando crea la rama y manda los cambios que estan en el stash
- git stash drop: Elimina el contenido del stash
- git stash drop stash@{<num_stash>}

## Git Clean: limpiar tu proyecto de archivos no deseados

Si por alguna razon se crean archivos que son un error entonces existe un comando que ayuda a eliminarlos:

- git clean → elimina los archivos que no estan trakeados, como por ejemplo cuando se hace una copia de algun archivo por error. El comando no funciona solo
- git clean —dry-run → Ejecucion en seco, simular lo que se va a borrar sin borrarlo
- git clean -f → Borrar lo archivos en cuestion
- Si se copia una carpeta git clean no lo va a identIficar puesto que ha git le importan los archivos no las carpetas

## Git cherry-pick: traer commits viejos al head de un branch

Si quiere traerme uno de los commits anteriores de una rama secundaria al master existe un comando para poder hacer esto:

- git cherry-pick

Si estoy trabajando en una rama que no he terminado pero se necesita un commit de la rama en el master pero como la historia esta adelantada pues no se hace el merge puesto que la rama no esta completa

En el master:

- git cherry-pick <hash del commit>

Cuando se haga un merge con la rama a la que se le hizo cherry-pick va a haber conflictos por el commit del cherry-pick puesto que hay dos ramas con las mismas lineas de texto 

## Reconstruir commits en Git con amend

Si al hacer un commits se olvida agregar algo y para que no quede evidencia de la equivocacion se usa el comando:

- Para usar el siguiente comando se deben hacer git add <archivo> para que los cambios queden en staging
- git commit —amend: Este comando permite agregar los cambios que estan en staging al commit anterior (Remendar un commit)

## Git Reset y Reflog: úsese en caso de emergencia

Cuando se usa el git log se ve el historial de todos los commits pero existe un comando que no olvida nada: 

- git reflog → Este comando muestra absolutamente todo el historial sin importar un si hubo un git reset
- Para devolverse a un commit anterior pero de manera que se devuelva la historia de mi repos debo usar:
    - git reset —hard <hash del commit>

**Nota**: git reset solo se debe usar en caso de emergencia, cuando realmente se rompio el codigo, siempre es mala practica modificar la historia del repositorio

## Buscar en archivos y commits de Git con Grep y log

- git grep <palabra> : Este comando se usa para buscar palabras dentro de un archivo y en donde aparece. El output es el lugar donde se uso la palabra en todos los archivos del repos.
- git grep -n <palabra>: Muestra el numero de la linea donde esta la palabra que se busca y que archivos
- git grep -c <palabra>:  Cuenta el numero de veces que se uso la palabra en el repositorio
- git log -S <palabra>: Busca cuantas veces se uso la palabra en los commits

## Comandos y recursos colaborativos en Git y GitHub

- git shortlog: Muestra cuantos commits ha hecho cada persona que ha aportado al repo
- git shortlog -sn : Muestra la informacion de manera mas  condensada
- git shortlog -sn —all: Muestra la cuenta de todos los commits incluyendo los que se borraron
- git shortlog -sn -all —no-merges: Muestra la cuenta de todos los commits pero sin incluir los merge
- git config —global alias.stats "shortlog -sn -all —no-merges" → Estadisticas de los commits
- git blame <archivo>: Quien tiene la culpa de que en el archivo en cuestion
- git blame -c <archivo>: Identa mejor el comando
- git <comando> —help : muestra el manual del comando en cuestion
- git blame <archivo> -L<# linea>,<#linea> : Con este comando muestra solo el git blame entre las lineas especificadas
- git branch -r → Ver las ramas remotas
- git branch -a → Ver todas las ramas, locales y remotas

Graficas en github interesantes en → Insights del repos

## El futuro

![Alt text](/Imagenes/Untitled_15.png)
