---
title: WSDL 18/19 - Teachers' Documentation 
---

## General structure of each repository
All the repositories will have a directory build where the files involved in testing the assignments will be kept. In specific assignments there can be separated files used for testing because of requeriments of other tools (example: maven in the third assignment)

## About the continuous integration service chosen: Semaphore
[Semaphore](https://semaphoreci.com/) has been chosen as the tool used to keep continuous integrated the repositories. To get started, login in their web with your github credentials and grant the permissions it requires. These permissions will be used to send mail notifications which can be disabled from the settings menu. On your first login in the service a windows will be shown to grant access to the services to all repositories you want to test. You can select them now, or add them manually later.

## Configuring builds for a repository on Semaphore
To start making tests continous integration in a repository, click on the top section on the "*Create new > Project*" and select the repository you want. If the repository is part of an organization you will need to have granted Semaphore access to it. You can do it in Github in your profile in "*Settings > Applications > Authorized OAuth Apps > Semaphore*" and on the bottom section you will see a.ll organizations you can grant access to. Click "*Grant*" to the organization of the subject to set up the repositories in semaphore. Keep in mind that these changes may take a few minutes to be shown in the semaphore webpage.

Once this is done and you have selected the specific repository you want, you will have to choose one branch to test, usually master, and the owner of the project in semaphore. After this, an automatic scan will start to detect the main language of the repository. You can skip this step if you want clicking "*Skip the analysis*" as you can select the language manually in the next screen.

Now you will select the specific characteristics of the build of each repository. It is divided in three sections:

Note: You can now select the language on a drop-down on the top. This language will be used to set up the specific environment needed to test that language. For tests that are not specific for a programming language select "*Other*"

### Setup

Instructions to be executed before doing any test task. These are usually configuration tasks for other files, set up variables, paths, etc.

For this specific use case of the subject, first grant execution permission to the scripts files used in the builds.
```bash
chmod +x ./build/scriptFile.sh
```
We will do a command like this for every bash file which is going to be used in the build directory of the repository
We will also create an empty file "*err*" to write the results of the tests if something goes wrong:
```bash
touch err
```

### Jobs
This instructions are the core of the continuous integration build and will mark the build as valid if all instructions are completed with exit status 0, or failed in any other case. Mainly we will call here the scripts we granted execution permissions in the setup step:
```bash
./build/ficheroTest.sh 2> err
```
We redirect the standard error output to the "*err*" file we created before. This is done to check later if there were any errors (the "*err*" file wont be emtpy) and to not fill the logs of the build with those error messages.

There is an option to create parallel jobs which would be executed at the same time. This can be used to speed up the process of testing. In this specific use case there doesnt seem to be a lot of opportunities to do something like that because most tests rely on the previous ones having passed, but it is interesting to mention because it can be helpful in the future in other tasks. 

### After Job
Finally, we configure the instructions to be executed when the build is finishing. In this case we will call the script file in charge of creating the comments in the pull-request tested in Github.
```bash
./build/comment.sh
```

## Variables de entornos utilizadas
Para el correcto funcionamiento de muchos de los archivos de prueba es necesario incluir información delicada como Tokens de autorización API y demás. Para ello Semaphore cuenta con un sistema de variables de entorno que podemos acceder desde la sección *Project Settings > Environment Variables* de cada uno de los proyectos de Integración Continua. Allí pulsaremos *+ Add* y añadiremos la variable **TOKEN** que tendra como valor la clave API del usuario a relizar los comentarios. Por último marcaremos la casilla *Encrypt content* para reforzar la seguridad de la misma. 

## Consulta de resultados de las builds
En el panel de control del proyecto en Semaphore se puede consultar el estado de todas las builds realizadas haciendo click en la rama que se quiera observar o de la Pull Request a revisar. Haciendo click en el estado de una build podremos la salida por pantalla que ha producido cada mandato de ejecución.






# Descripción de los tests de cada tarea de la asignatura
Aquí se describiran los ficheros de prueba de cada una de las tareas de una forma similar a pseudocodigo.

#### comment.sh
Este fichero es común a todas las tareas por lo que será descritó aqui de forma común
1. Comprueba si el fichero *err* existe y no está vacio
    1. Si existe se parsea su contenido con el mandato *sed* para reemplazar carácteres invalidos para el Json
    2. Si no existe se establece un mensaje de exito por defecto
2. Se realiza la petición API para enviar el comentario

## Tests tarea 1
En esta tarea se ejecuta un script simple que evalua el fichero CSV.
#### testCSV.sh
Language: Other
Setup:
Jobs:
After Job:
1. Inicializa la variable de error a 0
2. Obtiene mediante una petición API a GitHub los datos de la Pull Request que son parseados con jq y se obtiene el nombre de usuario
3. Se comprueba si existe el fichero NombreDeUsuario.csv
    1. Si no existe muestra un mensaje de error y sale
    2. Si existe comprueba si todas las lineas tienen dos campos
        1. Si no se cumple se muestra un mensaje de error y sale
        2. Si se cumple no hace nada
4. Termina y sale con estado el número de errores encontrados

## Tests tarea 2
En esta tarea para realizar los tests, se ejecuta un *jar* pre-compilado por parte del profesor y se analizan los ficheros entregados por el alumno. Este *jar* se encuentra en la carpeta test.

#### testAssignment2.sh
1. Inicializa variables de error a 0 y falso
2. Obtiene mediante una petición API a GitHub los datos de la Pull Request que son parseados con jq y se obtiene el nombre de usuario
3. Se comprueba si existe el fichero NombreDeUsuario.rdf
    1. Si no existe muestra un mensaje y activa una variable de error
4. Se comprueba si existe el fichero NombreDeUsuario.ttl
    1. Si no existe muestra un mensaje y activa una variable de error
5. Se comprueba si existe el fichero NombreDeUsuario.png
    1. Si no existe muestra un mensaje de error
6. Si los dos ficheros rdf y ttl existen se realizan los tests ejecutando un fichero jar
    1. El estado de salida del mandato de ejecución de los tests se añade a la variable de error
7. Sale con el estado de error acumulado

## Tests tarea 3
En esta tarea se compila el codigo del alumno usando maven y se proceden a ejecutar los tests.

#### compileTasks.sh
1. Inicializa variables de error a 0
2. Obtiene mediante una petición API a GitHub los datos de la Pull Request que son parseados con jq y se obtiene el nombre de usuario
3. Se comprueba si existe el directorio NombreDeUsuario-NumMatricula
    1. Si no existe muestra un mensaje y sale
    2. Si existe copia todos los ficheros del alumno al directorio src y compila con maven
        1. Si hay problemas en la compilación muestra mensaje y sale
        2. Si no hay errores de compilación se procede a ejecutar los tests
            1. Si los tests no termina correctamente se imprime mensaje de error
4. El programa termina y sale con el estado de error
