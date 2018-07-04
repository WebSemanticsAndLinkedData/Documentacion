---
title: WSLD 18/19 - Assignment 1 CI - Teachers' documentation
---

## Assignment 1

[Link to the repository of this assignment](https://github.com/WebServicesAndLinkedData/Assignment1)

## Configuration assignment 1
This task is tested by a single script which checks the CSV files using the command *"awk"*.

The variables *numberfields* and *file* can be easily modified to test for other files and/or different number of fields on each csv.

#### Language
Other

#### Setup
```
chmod +x ./build/testAssignment1.sh
chmod +x ./build/comment.sh
touch err
git remote add upstream https://github.com/WebServicesAndLinkedData/Assignment1 | (exit 0)
git fetch upstream
```
#### Job
```
diff_result=$(git -c core.fileMode=false diff master upstream/master build/)
if [ "$diff_result" = "" ] ; then (exit 0) ; else echo "Build files were modified\nRevert the changes and try again" > err ; BUILDFILESMODIFIED=1 ;  (exit 1) ;  fi
./build/testAssignment1.sh 2> err
```
#### After Job
```
cat err #CHECK THIS STEP TO SEE WHICH ERRORS OCCURRED
if [[ $BUILDFILESMODIFIED -ne 1 ]]; then ./build/comment.sh ; fi
```

## Script testAssignment1.sh

1. Initialize the exit value variable to 0
2. Makes an API request to get the username of the user doing the pull request, parses the Json with the command jq to obtain the value, and assigns it to a variable.
3. Checks if the files Username.csv exists
    1. If it doesn't, prints an error message and adds 1 to the exit variable.
    2. If it exists, it check with the command awk if it has the three fields.
        1. If it doesn't, it prints an error message and adds 1 to the exit value.
4. Checks if the file HandsOn.csv has the correct number of fields.
  1. If it doesn't, it prints an error message and adds 1 to the exit value.
5. The scripts exits with the exit variable value.
