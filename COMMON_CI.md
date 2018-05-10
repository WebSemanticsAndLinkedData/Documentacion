---
title: WSLD 18/19 - Common CI - Teachers' documentation
---

Here there will be detailed those scripts common in some or all tasks of continuous integration.

#### comment.sh
This scripts is the one in charge of consulting the "*err*" file and produce the comment in the GitHub pull request.
1. Checks if the file "*err*" files exists and is not empty
    1. If it does, it parses its content and assigns it to a variable. The parser replaces invalid characters for the Json using the command "*sed*"
    2. If it doesnt exist or is empty, it assigns to the text variable a default success message.
2. Finally, it sends an API request using "*curl*" to post the comment with a Json with the text of the comment.
