---
title: DOCUMENTACION ALUMNOS
---

# Introducción

En este documento se describira las tareas a realizar para la asignatura de Web Services and Linked Data del curso 2018/2019, asi como unas guias basicas de las herramientas a utilizar y su uso.

## Utilización básica de Git y GitHub

 * En caso de aun no tenerla, crear una cuenta de GitHub. Esta será necesaria para realizar las Pull-Request a los repositorios de las asignaturas. 
 * Instalar Git en vuestro sistema operativo. Existe una version portable para los que no quieran añadirlo a su espacio de trabajo.  
 * Configurar Git de forma basica con los mandatos siguientes:
 ```git
 $ git config --global user.name "Your username here"
 $ git config --global user.email your_mail@here.com
 ```
* Realizar una copia personal del repositorio desde GitHub con el botón fork en el extremo superior derecha, y añadirlo a la cuenta de usuario
* Obtener el enlace de clonación mediante https y clonar este repositorio personal desde el terminal git con el mandato:
```git
$ git clone url
```
* Configurar un flujo upstream al repositorio original con el siguiente mandato:
```git
$ git remote add upstream https://github.com/FacultadInformatica-LinkedData/Curso2017-2018
```
Con esto el directorio para trabajar ya estaria listo, accede al mismo con el mandato cd y usa git de forma basica como se indica en esta guia [git basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
Para sincronizar el repositorio local con el original realizar:
```git
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
```
Estos pasos se tendran que realizar con cada uno de los repositorios de las tareas

## Acerca de la estructura del repositorio

La estructura de la organización de la asignatura estará dividida en diferentes repositorios donde se subiran los ficheros relevantes de cada una de las tareas, y a los cuales habra que subir el trabajo realizado por los alumnos.

## Acerca de las entregas

La entrega de las tareas se realizara mediante la interfaz web de GitHub, realizando una Pull-Request al repositorio principal de la asignatura. Para esto los alumnos despues de realizar los pasos descritos en la sección inicial sobre git deberan realizar push a su repositorio personal
```
$ git add [archivos a entregar]
$git commit -m "mensaje descriptivo"
$git push
```
Una vez realizado esto, acceder al repositorio desde la interfaz web de Github y realizar una Pull-Request pulsando el botón con ese mismo nombre debajo del botón para clonar.

## Acerca de la Integración Continua y las pruebas

Para cada tarea de la asignatura, tras la realización de cada Pull-Request o la actualización de los ficheros de la misma, un servicio externo evaluara automaticamente el estado del repositorio para comprobar que se hayan entregado los ficheros con la denominación correcta. Además, en algunos casos se pasaran tests mas especificos para detectar errores y comprobar el correcto funcionamiento de los entregables. Estos resultados se veran reflejados en un comentario en la misma Pull-Request, desde la cual tambien es posible consultar los logs de los tests realizados visitando el link que aparecera en las Pull-Requests.

# Tareas
Descripción específica de cada tarea a realizar y los tests que serán realizados.

## Tarea 1
Tarea de introducción. El fichero a entregar es un csv con el nombre del usuario de GitHub de la forma NombreDeUsuario.csv en la raiz del escritorio. Este csv contendrá dos campos, que serán el mismo nombre de usuario de Github otra vez y en la segunda columna el número de matricula de la universidad.

Test realizados:
* El fichero csv existe y se llama de forma correcta
* El fichero csv tiene dos campos

**ATENCIÓN: Es importante que estos campos sean correctos ya que otras tareas dependeran de ellos.**

## Tarea 2

Esta tarea consiste en crear un pequeño conjunto de datos en formato rdf y ttl, asi como un grafo de los mismos en formato png. Los archivos se subiran en la raiz del repositorio y se llamaran de la misma forma que el nombre de usuario del estudiante, de la forma NombreDeUsuario.png, NombreDeUsuario.rdf, NombreDeUsuario.ttl.

Test realizados:
* Los ficheros png, rdf y ttl existen y tienen el nombre correcto
* Los ficheros rdf y ttl son validos sintacticamente

## Tarea 3

Esta tarea consiste en realizar un codigo java usando la libreria Jena para trabajar con conjuntos de datos. Los archivos a completar se encuentran en src/main/java/upm/oeg/wsld/jena y son los denominados Task06 y Task07. Estos mismo archivos completados por el alumno se entregaran en un directorio en la raiz del repositorio denominado como el nombre de usuario de GitHub del alumno y su numero de matricula, de la forma siguiente: NombreDeUsuario-123456, en el cual se encontraran los ficheros Task06 y Task07 con ese nombre. El numero de matricula debe de ser el mismo que fue indicado en la tarea 1.

Test realizados:
* El directorio del alumno existe
* Los ficheros Task06 y Task07 se encuentran en dicho directorio
* Los ficheros de las tareas compilan correctamente
* Los ficheros pasan los tests de JUnit que se encuentran en src/test/java/upm/oeg/wsld/jena
