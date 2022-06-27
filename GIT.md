# **_GIT_**: **Sistema de control de versiones**

Es una aplicación que permite gestionar los cambios que se realizan sobre los elementos de un proyecto o repositorio, guardando así versionesd del mismo en todas sus fases de desarrollo.

---
## Creacion de repostiorios ✅
```
git init <nombre-repositorio>
```
Crea un repositorio nuevo con el nombre `<nombre-repositorio>`.

---
## Copia de repositorios ♻️
```
git clone <url-repositorio>
```
Crea una copia local del repositorio
ubicado en la dirección `<url-repositorio>`. Los dos repositorios, el original y la copia,
son independientes.

---
## Añadir cambios a la zona de intercambio temporal
```
git add 
```
- `git add <fichero>` añade cambios en el `<fichero>` del directorio de trabajo a la zona de intercambio temporal.
- `git add <carpeta>` añade los cambios en todos los ficheros de la `<carpeta>` del directorio de trabajo a la zona de intercambio temporal (_stage_).
- `git add .` añade todos los cambios de todos los ficheros no guardados aún en la zona de intercambio temporal.

---
## Añadir cambios al repositorio 🌎
```
git commit
```
- `git commit -m "mensaje"` confirma todos los cambios de la zona de intercambio temporal añadiéndolas al repositorio y **creando una nueva versión del proyecto**. `"mensaje"` es una descripción de ese cambio realizado en la nueva versión del proyecto.
- `git commit --amend -m "mensaje"` cambia el mensaje del último _commit_ por el nuevo mensaje `"mensaje"`.

---
FOTO

---
## Registro de cambios
Para guardar los cambios en un repositorio Git utiliza una estructura de tres
niveles:
- **Commit** ➡️ contiene información sobre el autor, el momento y el mensaje
de los cambios.
- **Árbol (_tree_)** ➡️ cada commit contiene además un árbol donde se registran los nombres y rutas de los ficheros en los repositorios cuando se hizo el _commit_.
- **_Blob (binary file object)_** ➡️ Para cada uno de los ficheros listados en el árbol hay un _blob_, que contiene una instantánea comprimida del contenido del fichero cuando se hizo el _commit_.
Si un fichero del repositorio no ha cambiado en el commit, el árbol apunta al blob del fichero del último _commit_ donde el fichero cambió.

---
## Referenciar un _commit_
Cada _commit_ tiene asociado un código _hash_ de 40 caracteres
hexadecimales que lo identifica de manera única. Hay dos formas de
referirse a un _commit_:
- **Nombre absoluto**: Se utiliza su código _hash_ (basta indicar los 4 o 5 primeros dígitos).
- **Nombre relativo**: Se utiliza la palabra **HEAD** para referirse siempre al último _commit_. Para referirse al penúltimo commit se utiliza **HEAD~1**, al antepenúltimo **HEAD~2**, etc.

---
FOTO

---
## Estado e historia de un repositorio❗

### 🔹Mostrar el estado de un repositorio

```
git status
```
- `git status` muestra el estado de los cambios en el repositorio desde la última versión guardada. En particular, muestra los ficheros con cambios en el directorio de trabajo que no se han añadido a la zona de
intercambio temporal y los ficheros en la zona de intercambio temporal
que no se han añadido al repositorio.

### 🔸Mostrar el historial de versiones de un repositorio
```
git log
```
- `git log` muestra el historial de commits de un repositorio ordenado
cronológicamente. Para cada commit muestra su código _hash_, el autor, la
fecha, la hora y el mensaje asociado.

    Este comando es muy versátil y muestra la historia del repositorio en
distintos formatos dependiendo de los parámetros que se le den. Los
más comunes son:

  - `--oneline` muestra cada _commit_ en una línea produciendo una salida más compacta.
  - `--graph` muestra el historial en forma de grafo.

### 🔹Mostrar los datos de un _commit_
```
git show
```
- `git show` muestra el usuario, el día, la hora y el mensaje del último
_commit_, así como las diferencias con el anterior.
- `git show <commit>` muestra el usuario, el día, la hora y el mensaje del _commit_ indicado, así como las diferencias con el anterior.

### 🔸Mostrar el historial de cambios de un fichero
```
git annotate
```
- `git annotate` muestra el contenido de un fichero anotando cada línea
con información del _commit_ en el que se introdujo.

  Cada línea de la salida contiene los 8 primeros dígitos del código _hash_ del _commit_ correspondiente al cambio, el autor de los cambios, la fecha, el número de línea del fichero y el contenido de la línea.

### 🔹Mostrar las diferencias entre versiones
```
git diff
```
- `git diff` muestra las diferencias entre el directorio de trabajo y la zona de intercambio temporal.
- `git diff --cached` muestra las diferencias entre la zona de
intercambio temporal y el último _commit_.
- `git diff HEAD` muestra la diferencia entre el directorio de trabajo y el último _commit_.

---
## Deshacer cambios 🔙

### 🔸Eliminar cambios del directorio de trabajo o volver a una versión anterior
```
git checkout
```
- `git checkout <commit> -- <file>` actualizo el fichero `<file>` a la versión correspondiente al `<commit>`.
  
  Suele utilizarse para eliminar los cambios en un fichero que no han sido guardadso aún en la zona de intercambio temporal, mediante el comando `git checkout HEDA -- <file>`.

### 🔹Eliminar cmabios de la zona de intercambio temporal
```
git reset
```
- `git reset <fichero>` elimina los cambios del fichero `<fichero>` de la zona de intercambio temporal, pero preserva los cambios en el
directorio de trabajo.

  ⚠️ Para eliminar por completo los cambios de un fichero que han sido
guardados en la zona de intercambio temporal hay que aplicar este
comando y después `git checkout HEAD -- <fichero>`.

### 🔸Eliminar cmabios de un _commit_
```
git reset
```
- `git reset --hard <commit>` elimina todos los cambios desde el
_commit_ <commit> y actualiza el HEAD de este _commit_.

  ☢️ ¡Ojo! Usar con cuidado este comando pues los cambios posteriores al
_commit_ indicado se pierden por completo.

  Suele usarse para eliminar todos los cambios en el directorio de trabajo
desde el último _commit_ mediante el comando `git reset --hard
HEAD`.

- `git reset <commit>` actualiza el HEAD al _commit_ `<commit>`, es decir, elimia todos los _commits_ psoteriores a este, pero no elimina los cambios del directorio de trabajo.

---

## Ramas 🌳
Inicialmente cualquier repositorio tiene una única rama llamada **_master_** donde se van sucediendo todos los commits de manera lineal.

GIT permite la cración de ramas para trabajar distintas versiones de un proyecto a la vez. Nos permite añadir nuevas funcionalidades al proyecto sin qu interfieran con lo desarrollado hasta ahora.

Cuando se termina el desarrollo de las nuevas funcionalidades, las ramas se pueden fusionar para incorporar los cambios al proyecto principal.

### 🐟 Creación de ramas
```
git branch
```
- `git branch <rama>` crea una rama con el nombre `<rama>` en el repositorio a partir del último _commit_, es decir, donde apunte HEAD.

  Al crear una rama a partir de un _commit_, el flujo de _commits_ se bifurca en dos de manera que se pueden desarrollar dos versiones del proyecto en paralelo.

---
FOTOS

---
### 🐬 Listado de ramas
```
git log
```
- `git branch` muestra las ramas activas de un repositorio indicando con `*` la rama activa en ese momento.
- `git log --graph --oneline` muestra la historia del repositorio en forma de grafo incluyendo todas las ramas.

### 🐳 Fusión de ramas
```
git merge
```
- `git merge <rama>` integra los cambios de la `<rama>` en la rama actual a la que apunta HEAD.

---
FOTO

---
## Resolución de conflictos 🛑
Para fusionar dos ramas es necesario que no haya conflictos entre los
cambios realizados a las dos versiones del proyecto.

Si en ambas versiones se han hecho cambios sobre la misma parte de un
fichero, entonces se produce un conflicto y es necesario resolverlo antes de poder fusionar las ramas.

La resolución debe hacerse manualmente observando los cambios que
intereren y decidiendo cuales deben prevalecer, aunque existen
herramientas como **KDif3** o **meld** que facilitan el proceso.

### 🔹Reorganización de ramas
```
git rebase
```
- `git rebase <rama-1> <rama-2>` replica los cambios de la rama
`<rama-2>` en la rama `<rama-1>` partiendo del ancestro común de
ambas ramas. El resultado es el mismo que la fusión de las dos ramas
pero la bifurcación de la `<rama-2>` desaparece ya que sus _commits_
pasan a estar en la `<rama-1>`.

### 🔸Eliminación de ramas
```
git branch -d
```
- `git branch -d <rama>` elimina la rama de nombre `<rama>` siempre y
cuando haya sido fusionada previamente.
- `git branch -D <rama>` elimina la rama de nombre `<rama>` incluso si
no ha sido fusionada. Si la rama no ha sido fusionada previamente se
perderán todos los cambios de esa rama.

---
## Respositorios remotos
La otra característica de GIT, que unida a las ramas, facilita la colaboración entre distintos usuarios en un proyecto son los repositorios remotos.

GIT permite la creación de una copia del repositorio en un servidor git en internet. La principal ventaja de tener una copia remota del repositorio, a parte de servir como copia de seguridad, es que otros usuarios pueden acceder a ella y hacer también cambios.

### 🔹Añadir un repositorio remoto
```
git remote add
```
- `git remote add <repositorio-remoto> <url>` crea un enlace
con el nombre `<repositorio-remoto>` a un repositorio remoto
ubicado en la dirección `<url>`.

  ▶️ Cuando se añade un repositorio remoto a un repositorio, GIT seguirá
también los cambios del repositorio remoto de manera que se pueden
descargar los cambios del repositorio remoto al local y se pueden subir los cambios del repositorio local al remoto. ◀️

### 🔸Lista de repositorios remotos
```
git remote
```
- `git remote` muestra un listado con todos los enlaces a repositorios
remotos denidos en un repositorio local.
- `git remote -v` muestra además las direcciones url para cada
repositorio remoto.

### 🔹Descargar cambios desde un repositorio remoto
- `git pull <remoto> <rama>` descarga los cambios de la rama `<rama>`
del repositorio remoto `<remoto>` y los integra en la última versión del
repositorio local, es decir, en el HEAD.
- `git fetch <remoto>` descarga los cambios del repositorio remoto
`<remoto>` pero no los integra en la última versión del repositorio local.

### 🔸Subir cambios a un repositorio remoto
```
git push
```
- `git push <remoto> <rama>` sube al repositorio remoto `<remoto>`
los cambios de la rama `<rama>` en el repositorio local.

### 🔹Colaboración en repositorios remotos de GitHub
Existen dos formas de colaborar en un repositorio alojado en GitHub: 

- Ser colaborador del repositorio.
  1. Recibir autorización de colaborador por parte del propietario del proyecto.
  2. Clonare el repositorio en local.
  3. Hacer cambios en el repositorio local.
  4. Subir los cambios al repositorio remoto.

- Replicar el repositorio y solicitar integración de cambios.
  1. Replicar el repositorio remoto en nuestra cuenta de GitHub mediante un **_fork_**.
  2. Hacer cambios en nuestro repositorio remoto.
  3. Solicita al propietario del repositorio original que integre nuestros cambios en su repositorio mediante un **_pull request_**.

---

#### REFERENCIAS: 
- [Manual Git](manual-git.pdf)
- [Git](git.pdf)
---