# GAMESS COMMON Block variable declartions

This directory is intended for storing GAMESS COMMON block variable declarations.

It is intended to help developers adhere to the coding policy of `IMPLICIT NONE`

*  Give each common block a markdown file extension (.md).
*  Use the following markdown format for the Fortran code:

    ```
       ```fortran
       COMMON /<NAME>/ <VARIABLE(S)>
      *                <VARIABLE(S)>
       
       <TYPE> <VARIABLE(S)>
       ```
    ```

*  Variable declarations should follow the same order as they appear in the COMMON block list.
