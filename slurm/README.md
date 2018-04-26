# gms.interactive

Usage information:
`gms.interactive`

Example:
*  Submit a job using exam01.inp with 1 hr walltime and an MPI build of GAMESS:

   `gms.interactive exam01 -w 1:0:0 -mpi`

Examples:
*  Submit a job using exam01.inp with 1 hr walltime and a sockets build of GAMESS:

   `gms.interactive exam01 -w 1:0:0 -sockets`

   or

   `gms.interactive exam01 -w 1:0:0`

# CyEnce
*  Create a bin folder in your home directory:

   `mkdir $HOME/bin`

*  Add **$HOME/bin** to your path:

   `export PATH=$HOME/bin:$PATH`

*  Copy **gms.interactive** into **$HOME/bin**

*  Copy **rungms.interactive** into **$GMS_DIR** (GAMESS directory)

*  Use the `-exepath` flag to specify the path to the GAMESS directory where the **rungms.interactive** script exists (should be the same path used in the previous step).

   Example:

   `gms.interactive exam01 -w 1:0:0 -mpi -exepath /home/ssok1/dir.git.dev.gamess`

