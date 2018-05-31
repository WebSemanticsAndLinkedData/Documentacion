---
title: WSLD 18/19 - Assignment 2 CI - Teachers' documentation
---

## Assignment 2

[Link to the repository of this assignment](https://github.com/WebServicesAndLinkedData/Assignment2)

## Configuration assignment 2
In this task, in order to test the data files of the students, a jar will be executed with the tests pre-compiled. The code of the *jar* file can be found [here]( TODO )

#### Language
Java <br>
Version: 8u151

#### Setup
```
chmod +x ./build/testAssignment2.sh

chmod +x ./build/comment.sh

touch err
```
#### Job
```
diff_result=$(git diff build/)

if [ "$diff_result" = "" ] ; then (exit 0) ; else echo "Build files modified!!!\nRevert the changes and try again." > err ; (exit 1) ;  fi

./build/testAssignment2.sh 2> err
```
#### After Job
```
./build/comment.sh
```

## Script testAssignment2.sh
1. Initialize the exit value variable to 0
2. Makes an API request to get the username of the user doing the pull request, parses the Json with the command jq to obtain the value, and assigns it to a variable.
3. Checks if the files Username.rdf exists
    1. If it doesn't, prints an error message and adds 1 to the exit variable.
4. Checks if the files Username.ttl exists
    1. If it doesn't, prints an error message and adds 1 to the exit variable.
5. Checks if the files Username.png exists
    1. If it doesn't, prints an error message and adds 1 to the exit variable.
6. If both rdf and ttl files exist the jar is executed to test the data
    1. The exit status of the execution of the tests is added to the exit variable
7. The scripts exits with the exit variable value.
