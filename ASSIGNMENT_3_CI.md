---
title: WSLD 18/19 - Assignment 3 CI - Teachers' documentation
---

## Assignment 3

[Link to the repository of this assignment](https://github.com/WebServicesAndLinkedData/Assignment3)

## Configuration assignment 3
This tasks compiles the code submitted by the student using maven and then executes the JUnit tests located in src/test/java/upm/oeg/wsld/jena.

#### Language
Java <br>
Version: 8u151

#### Setup
```
chmod +x ./build/testAssignment3.sh

chmod +x ./build/comment.sh

touch err
```
#### Job
```
diff_result=$(git diff build/)

if [ "$diff_result" = "" ] ; then (exit 0) ; else echo "Build files modified!!!\nRevert the changes and try again." > err ; (exit 1) ;  fi

./build/testAssignment3.sh 2> err
```
#### After Job
```
./build/comment.sh
```

## Script testAssignment3.sh
1. Initialize the exit value variable to 0
2. Makes an API request to get the username of the user doing the pull request, parses the Json with the command jq to obtain the value, and assigns it to a variable.
3. Checks if the directory Username-StudentNumber exists
    1. If it doesn't, prints an error message and adds 1 to the exit variable.
    2. If it exists, it copies the files inside to the src directory.
        1. If there are problems with the compilations it prints an error message and exists.
        2. If it compiles correctly it proceeds to execute the tests.
            1. If there are errors in the tests, error messages are printed and the value of the exit variable is increased.
4. The scripts exits with the exit variable value.
