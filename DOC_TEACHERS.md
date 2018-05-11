---
title: WSDL 18/19 - Teachers' Documentation
---

## General structure of each repository
All the repositories will have a directory build where the files involved in testing the assignments will be kept. In specific assignments there can be separated files used for testing because of requeriments of other tools (example: maven in the third assignment)

## About the continuous integration service chosen: Semaphore
[Semaphore](https://semaphoreci.com/) has been chosen as the tool used to keep continuous integrated the repositories. To get started, login in their web with your github credentials and grant the permissions it requires. These permissions will be used to send mail notifications which can be disabled from the settings menu. On your first login in the service a windows will be shown to grant access to the services to all repositories you want to test. You can select them now, or add them manually later.

## Configuring builds for a repository on Semaphore
To start making tests continous integration in a repository, click on the top section on the "*Create new > Project*" and select the repository you want. If the repository is part of an organization you will need to have granted Semaphore access to it. You can do it in Github in your profile in "*Settings > Applications > Authorized OAuth Apps > Semaphore*" and on the bottom section you will see a.ll organizations you can grant access to. Click "*Grant*" to the organization of the subject to set up the repositories in semaphore. Now in the "*Create new > Project*" press the refresh button to see the organization added.

![Granting access to the organization in GitHub](https://raw.githubusercontent.com/WebServicesAndLinkedData/Documentacion/master/images/grantAccessSemaphore.png)<br>*Steps to access the granting access menu in GitHub website*

Once this is done and you have selected the specific repository you want, you will have to choose one branch to test, usually master, and the owner of the project in semaphore. After this, an automatic scan will start to detect the main language of the repository. You can skip this step if you want clicking "*Skip the analysis*" as you can select the language manually in the next screen.

Now you will select the specific characteristics of the build of each repository. It is divided in three sections:

Note: You can now select the language on a drop-down on the top. This language will be used to set up the specific environment needed to test that language. For tests that are not specific for a programming language select "*Other*"

### Setup

Instructions to be executed before doing any test task. These are usually configuration tasks for other files, set up variables, paths, etc.

For this specific use case of the subject, first grant execution permission to the scripts files used in the builds.
```
chmod +x ./build/scriptFile.sh
```
We will do a command like this for every bash file which is going to be used in the build directory of the repository
We will also create an empty file "*err*" to write the results of the tests if something goes wrong:
```
touch err
```

### Jobs
This instructions are the core of the continuous integration build and will mark the build as valid if all instructions are completed with exit status 0, or failed in any other case. Mainly we will call here the scripts we granted execution permissions in the setup step:
```
./build/ficheroTest.sh 2> err
```
We redirect the standard error output to the "*err*" file we created before. This is done to check later if there were any errors (the "*err*" file wont be emtpy) and to not fill the logs of the build with those error messages.

There is an option to create parallel jobs which would be executed at the same time. This can be used to speed up the process of testing. In this specific use case there doesnt seem to be a lot of opportunities to do something like that because most tests rely on the previous ones having passed, but it is interesting to mention because it can be helpful in the future in other tasks.

### After Job
Finally, we configure the instructions to be executed when the build is finishing. In this case we will call the script file in charge of creating the comments in the pull-request tested in Github.
```
./build/comment.sh
```

### After configuring the project

After having done this, an automatic first build will be launched. This build will fail, but even so it is important to not cancel it, otherwise next pull request will not trigger a build until this first build is finished.

## Environment variables
For the correct functioning of some scripts it is needed to include sensitive information as authorization tokens to make api requests. This values cannot be stored in plaintext in the scripts directly as it would be a security risk, so we use the environment variables feature in Semaphore.

Under every repository we can go to the section "*Project Settings > Environment Variables*" and setup there all the variables needed for the tests. In this specific use case we will press *+ Add* and create a environment variable called "**TOKEN**" with value the actual string of characters that represent the token authorization of the github user to create the comments. Finally, check the "*Encrypt content*" to make the variable more secure in case of security flaws.

Note: The github api token can be acquired in Github in "*Settings > Developer Settings > Personal access tokens*". It is recommended to have a dummy or specific user for this as in case the token is leaked there is no risk involving the ownership of the repositories.

## Consulting the result of the builds
In the dashboard in the main page of semaphore you can see listed all repositories added and a symbol indicating the result of the latest build tested. Clicking on each repository you can see a detailed view of all actions taken, including builds, and you can click them to consult the logs the build generated.

# Description of the test of each assignment
Here there is a list of links to the specific documentation about the continuous integration of each task.

 * [Common test files to all tasks](https://webservicesandlinkeddata.github.io/Documentacion/COMMON_CI)
 * [Assignment 1 CI](https://webservicesandlinkeddata.github.io/Documentacion/ASSIGNMENT_1_CI)
 * [Assignment 2 CI](https://webservicesandlinkeddata.github.io/Documentacion/ASSIGNMENT_2_CI)
 * [Assignment 3 CI](https://webservicesandlinkeddata.github.io/Documentacion/ASSIGNMENT_3_CI)
