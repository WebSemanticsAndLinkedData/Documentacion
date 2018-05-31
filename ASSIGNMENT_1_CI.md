---
title: WSLD 18/19 - Assignment 1 CI - Teachers' documentation
---

## Assignment 1

[Link to the repository of this assignment](https://github.com/WebServicesAndLinkedData/Assignment1)

## Configuration assignment 1
This task is tested by a single script which checks the CSV files using the command *"awk"*.

#### Language
Other

#### Setup
```
chmod +x ./build/testAssignment1.sh

chmod +x ./build/comment.sh

touch err
```
#### Job
```
diff_result=$(git diff build/)

if [ "$diff_result" = "" ] ; then (exit 0) ; else echo "Build files modified!!!\nRevert the changes and try again." > err ; (exit 1) ;  fi

./build/testAssignment1.sh 2> err
```
#### After Job
```
./build/comment.sh
```

## Script testAssignment1.sh

1. Initialize the exit value variable to 0
2. Makes an API request to get the username of the user doing the pull request, parses the Json with the command jq to obtain the value, and assigns it to a variable.
3. Checks if the files Username.csv exists
    1. If it doesn't, prints an error message and adds 1 to the exit variable.
    2. If it exists, it check with the command awk if it has two fields.
        1. If it doesn't, it prints an error message and adds 1 to the exit value.
        2. If it does, it continues.
4. The scripts exits with the exit variable value.
