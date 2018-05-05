---
title: WSLD 18/19 - Students' documentation
---

## Basic guide to Git and GitHub

 * First of all, create a Github account. It is totally free and you need it to hand the assignments of the subject. 
 * Download and install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) in your operative system. If you don't want to pollute your global workspace with it, there is available a portable version which doesn't need installation.  
 * Start the git bash and configure your authentication credentials:
 ```git
 $ git config --global user.name "Your username here"
 $ git config --global user.email your_mail@here.com
 ```
 * In the github page of the repository, fork it with the button at the top-right of the screen [TODO] and add it to your account. This repository will be your personal version where you will add your change before submiting them to the subject's one.
 * Clone your personal version of the repository. This will make a local copy of the repository, where you will make changes before uploading it to your remote personal version of the repository. First copy the clone url with the green button using HTTPS [TODO]. Then use the next command in your git bash to download it to your computer:
```git
$ git clone url
```

From here on you need to use these commands inside the directory of the cloned repository. Use cd to change directory.

* Configure an upstream to the original repository of the subject. This will be used to update your local version of the repository with the changes made in the official one. Use the next command in your git bash :
```git
$ git remote add upstream https://github.com/FacultadInformatica-LinkedData/Curso2017-2018
```
Now everything is ready to use. You can learn the basics of how git works with this [git guide](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics).
To sync your local repository with the new changes in the official one use the next commands
```git
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
```
The steps shown here must be used with each of the repositories of the assignments.

## About the structure of the repositories

The structure of the organization will be split in different repositories for each one of the assignments. You will have to do the previously written steps for all of them and upload your work according to the guidelines of each one of the assignments, which will be specified in the same repository and here.

## About submitting your work 

The upload of your work will have to follow the standard procedure to contributing to a repository in github. This means you need to fork the repository and clone it in your computer, add and make the changes in the files involved, commit and upload them to your remote copy of the repository, and create a pull-request to the repository of the subject to be accepted by the teachers.

When you have done your changes, add and upload your files to your copy of the repository with these commands:
```
$ git add [file to upload]
$ git commit -m "descriptive message"
$ git push
```
Once this is done, from your browser navigate to your github repository and submit it with the pull-request button [TODO]

## About the continuous integration and tests

After doing a pull request for any of the repositories of the subject, a configured service will test those files and check if they are valid. These tests can range from checking if the files exist, to run code and unitary test to see the correct behaviour of the submitted code. What is expected of your work from the point of view of these tests will be specified in the section of the corresponding assignment.

After these tests have passed, a message will be submitted to your pull request informing of the results, as well as a message of what errors have happened in case there have been any.

# Assignments
You can find descriptions of each one of the assignments in the next links:

 * [Assignment 1] TODO
 * [Assignment 2] TODO
 * [Assignment 3] TODO
 
 
 
 
 
 
 
 
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
