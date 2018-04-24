---
title: DOCUMENTACIÓN PROFESORES
---

# Acerca del sistema de integración continua elegido: Semaphore
[Semaphore](https://semaphoreci.com/) ha sido elegido como la alternativa para realizar la integración continua de las tareas de la asignatura. Para comenzar, acceded a la web, hacer Log In con la cuenta de GitHub y concerde los permisos que solicita. Estos permisos se utilizan principalmente para enviar correos de notificación de las builds, que pueden ser desactivados en cualquier momento. Al iniciar sesión por primera vez se preguntara por el acceso a los repositorios y organizaciones que se quiere concederle, que pueden ser cambiado en cualquier momento mas tarde.

## Creación de builds para un repositorio en Semaphore
Para comenzar a realizar Integración continua sobre un repositorio, seleccionar en la parte superior de la web el botón de *Create New > Project*. Desde esa pantalla añadir el repositorio que se quiera en la sección correspondiente de la organización. En caso de que la organización no aparezca deberemos darle permisos, para ello, acudiremos a GitHub y accederemos en nuestro perfil *Settings > Applications > Authorized OAuth Apps > Semaphore* y en la parte inferior veremos todas las organizaciones a las se pertenece y daremos acceso con el botón *Grant* correspondiente de la misma.

Una vez hecho esto, quizás tengamos que esperar unos minutos para que los cambios se vean reflejados en la web de semaphore, pero cuando lo esten, seleccionar el respositorio que se quiere integrar, asi como la rama principal de prueba y el propietario del proyecto.
Después de esto, un escaneo automático comenzará para detectar el lenguaje por defecto, que podemos omitir pulsando *Skip the analysis* e indicarlo manualmente en la siguiente pantalla.
En esta pantalla realizaremos la configuración de prueba de la build. Se divide en tres secciones principales:

### Setup

Instrucciones a ejecutar antes de realizar las tareas de prueba. Dado que estan tareas van a ser ejecutadas desde un script debemos darles accesos de ejecución con la instrucción:
```bash
chmod +x fichero.sh
```
Haremos esto por cada fichero bash que vayamos a ejecutar y tengamos en la carpeta build del repositorio.
Además crearemos el fichero donde escribiremos los mensajes de error para más tarde leerlo y formar el comentario:
```bash
touch err
```

### Jobs

### After Job

## Variables de entornos utilizadas
Para el correcto funcionamiento de muchos de los archivos de prueba es necesario incluir información delicada como Tokens de autorización API y demás. Para ello Semaphore cuenta con un sistema de variables de entorno que podemos acceder desde la sección *Project Settings > Environment Variables* de cada uno de los proyectos de Integración Continua. Allí pulsaremos *+ Add* y añadiremos la variable **TOKEN** que tendra como valor la clave API del usuario a relizar los comentarios. Por último marcaremos la casilla *Encrypt content* para reforzar la seguridad de la misma. 

## Consulta de resultados de las builds

# Descripción de los tests de cada tarea de la asignatura

## Tests tarea 1

## Tests tarea 2

## Tests tarea 3
