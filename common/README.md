# GAMESS COMMON Block variable declartions

This directory is intended for storing GAMESS COMMON block variable declarations.

It is intended to help developers adhere to the coding policy of `IMPLICIT NONE`.

*  Give each common block a markdown file extensions.
*  Use the following markdown format for the Fortran code:

    ```
       ```fortran
       COMMON /<NAME>/ <VARIABLE(S)>
      *                <VARIABLE(S)>
       
       <TYPE> <VARIABLE(S)>
       ```
    ```
