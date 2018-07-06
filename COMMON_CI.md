---
title: WSLD 18/19 - Common CI - Teachers' documentation
---

Here there will be detailed those scripts common in some or all tasks of continuous integration.

#### comment.sh
This script is the one in charge of consulting the "*err*" file and produce the comment in the GitHub pull request.
1. Checks if the file "*err*" files exists and is not empty
    1. If it does, it parses its content and assigns it to a variable. The parser replaces invalid characters for the Json using the command "*sed*"
    2. If it doesnt exist or is empty, it assigns to the text variable a default success message.
2. Finally, it sends an API request using "*curl*" to post the comment with a Json with the text of the comment.

### generateReport.sh
This script checks the result of the build on the *err* file and writes a line in the student's own csv file of the first assignment informing of when was it last updated, and if the build was succesful or with errors.
1. Gets the name of the user doing the pull request
2. Configures the git servicem
3. Clones the Assignment 1 repository and goes inside it
4. Check if the student's csv file exists
    1. If the file does not exist, the creation of the report is aborted.
5. Gets the current date
6. Removes the previous report line of the assignment being reported if it exists
7. Checks if the *err* file is empty or not
    1. If it is empty, the message is set to "Submitted succesfully"
    2. If it is not empty because there has been errors, the message is set to "Submitted with errors"
8. The file is added, committed, and pushed to the main repository, with a comment explaining the update, and the "[ci skip]" text to avoid a new CI build because of the update commit.
