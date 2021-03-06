---
title: WSDL 18/19 - Teachers' Documentation
---

## General structure of each repository
All the repositories will have a directory build where the files involved in testing the assignments will be kept. In specific assignments there can be separated files used for testing because of requirements of other tools (example: maven in the third assignment)

## About the continuous integration service chosen: Semaphore
[Semaphore](https://semaphoreci.com/) has been chosen as the tool used to keep continuous integrated the repositories. To get started, login in their web with your github credentials and grant the permissions it requires. These permissions will be used to send mail notifications which can be disabled from the settings menu. On your first login in the service a windows will be shown to grant access to the services to all repositories you want to test. You can select them now, or add them manually later.

## Configuring builds for a repository on Semaphore
To start making tests of continuous integration in a repository, click on the top section on the "*Create new > Project*" and select the repository you want. If the repository is part of an organization you will need to have granted Semaphore access to it. You can do it in GitHub in your profile in "*Settings > Applications > Authorized OAuth Apps > Semaphore*" and on the bottom section you will see all organizations you can grant access to. Click "*Grant*" to the organization of the subject to set up the repositories in semaphore. Now in the "*Create new > Project*" press the refresh button to see the organization added.

![Granting access to the organization in GitHub](https://raw.githubusercontent.com/WebSemanticsAndLinkedData/Documentacion/master/images/grantAccessSemaphore.png)<br>*Steps to access the granting access menu in GitHub website*

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
We will also add an upstream to the original repository to check the original files the pull-request is based on. An (exit 0) is added in case the upstream is already defined, so the setup command never fails (otherwise the build will be stopped before even start).
```
git remote add upstream https://github.com/WebSemanticsAndLinkedData/XXXXX | (exit 0)
git fetch upstream
```

### Jobs
This instructions are the core of the continuous integration build and will mark the build as valid if all instructions are completed with exit status 0, or failed in any other case. Mainly we will call here the scripts we granted execution permissions in the setup step.

First of all, we need to check if the build files have been modified. The way all Continuous Integration systems work is that they test the files submitted by the user, so if the tests have been altered the results could be incorrect. This can be prevented by checking with some instructions in semaphore to see if the files have been modified.
```
diff_result=$(git -c core.fileMode=false diff master upstream/master build/)

if [ "$diff_result" = "" ] ; then (exit 0) ; else echo "Build files were modified\nRevert the changes and try again" > err ; BUILDFILESMODIFIED=1 ;  (exit 1) ;  fi
```

This instructions will check the difference between the remote build files and the ones submitted by the student, and will exit with 1 if they have been modified, printing an error message to the *err* file.

More directories to be checked can be added concatenating instructions in the diff_results line.

After we have made sure the build files are the correct ones we can execute the tests with the following command:
```
./build/scriptFile.sh 2> err
```
We redirect the standard error output to the "*err*" file we created before. This is done to check later if there were any errors (the "*err*" file wont be emtpy) and to not fill the logs of the build with those error messages and just keep the standard output.

There is an option to create parallel jobs which would be executed at the same time. This can be used to speed up the process of testing. In this specific use case there doesn't seem to be a lot of opportunities to do something like that because most tests rely on the previous ones having passed, but it is interesting to mention as it can be helpful in the future in other tasks.

### After Job
Finally, we configure the instructions to be executed when the build is finishing. In this case we will call the script files in charge of creating the comments in the pull-request tested in Github as well as generating the report in the student's csv file. These scripts are only called if the build files have not been modified. This is a security measure.

The file *err* is also printed to help the user visualize it.
```
cat err #CHECK THIS STEP TO SEE WHICH ERRORS OCCURRED
if [[ $BUILDFILESMODIFIED -ne 1 ]]; then ./build/comment.sh ; fi
if [[ $BUILDFILESMODIFIED -ne 1 ]]; then ./build/generateReport.sh ; fi
```

NOTE: For specific tasks the reports are not generated. See the last section in this document for the specifics of each project.

### After configuring the project

After having done this, an automatic first build will be launched. This build will always fail, but it is important to not cancel it, otherwise next pull request will not trigger a build until this first build is finished.

## Environment variables
For the correct functioning of some scripts it is needed to include sensitive information as authorization tokens to make api requests. This values cannot be stored in plaintext in the scripts directly as it would be a security risk, so we use the environment variables feature in Semaphore.

Under every repository we can go to the section "*Project Settings > Environment Variables*" and setup there all the variables needed for the tests. In this specific use case we will press *+ Add* and create a environment variable called "**TOKEN**" with value the actual string of characters that represent the token authorization of the github user to create the comments. Finally, check the "*Encrypt content*" to avoid revealing it.

Note: The github api token can be acquired in Github in "*Settings > Developer Settings > Personal access tokens*". It is recommended to have a dummy or specific user for this with the correct privileges as in case the token is leaked there is no risk involving the ownership of the repositories.

## Consulting the result of the builds
In the dashboard in the main page of semaphore you can see listed all repositories added and a symbol indicating the result of the latest build tested. Clicking on each repository you can see a detailed view of all actions taken, including builds, and you can click them to consult the logs the build generated.

# Description of the test of each assignment
The contents described here are general guidelines for all projects. Specific definitions of each task continuous integration can be found here:

 * [Common test files to all tasks](https://websemanticsandlinkeddata.github.io/Documentacion/COMMON_CI)
 * [Assignment 1 CI](https://websemanticsandlinkeddata.github.io/Documentacion/ASSIGNMENT_1_CI)
 * [Assignment 2 CI](https://websemanticsandlinkeddata.github.io/Documentacion/ASSIGNMENT_2_CI)
 * [Assignment 3 CI](https://websemanticsandlinkeddata.github.io/Documentacion/ASSIGNMENT_3_CI)
 * [HandsOn CI](https://websemanticsandlinkeddata.github.io/Documentacion/HANDSON_CI)
