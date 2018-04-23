---
title: DOCUMENTACION ALUMNOS
---

# Introducción

En este documento se describira las tareas a realziar para la asignatura de Web Services and Linked Data del curso 2018/2019, asi como unas guias basicas de las herramientas a utilizar y su uso.

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

La estructura de la organización de la asignatura estará dividida en diferentes repositorios donde se subiran los entregables de cada tarea correspondiente de la forma que se explicará a continuación.

## Acerca de las entregas

La entrega de las tareas se realizara mediante la interfaz web de GitHub, realizando una Pull-Request al repositorio principal de la asignatura. Para esto los alumnos deberan hacer un fork propio de cada uno de los repositorios en su propia cuenta de usuario.

## Acerca de la Integración Continua y las pruebas

Para cada tarea de la asignatura, tras la realización de cada Pull-Request o la actualización de los ficheros de la misma, un servicio externo evaluara automaticamente el estado del repositorio para comprobar que se hayan entregado los ficheros con la denominación correcta, ademas de en algunos casos se pasaran tests mas especificos para detectar errores. Estos resultados se veran reflejados en un comentario en la misma Pull-Request. Además, los alumnos puede consultar los logs de los tests visitando el link que aparecera en las Pull-Requests.

# Tareas

## Tarea 1

## Tarea 2

## Tarea 3
