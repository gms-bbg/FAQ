# gms.interactive

Usage information:
```
gms.interactive

   ÛÛÛÛÛÛÛÛÛ    ÛÛÛÛÛÛÛÛÛ   ÛÛÛÛÛÛ   ÛÛÛÛÛÛ ÛÛÛÛÛÛÛÛÛÛ  ÛÛÛÛÛÛÛÛÛ   ÛÛÛÛÛÛÛÛÛ 
  ÛÛÛ°°°°°ÛÛÛ  ÛÛÛ°°°°°ÛÛÛ °°ÛÛÛÛÛÛ ÛÛÛÛÛÛ °°ÛÛÛ°°°°°Û ÛÛÛ°°°°°ÛÛÛ ÛÛÛ°°°°°ÛÛÛ
 ÛÛÛ     °°°  °ÛÛÛ    °ÛÛÛ  °ÛÛÛ°ÛÛÛÛÛ°ÛÛÛ  °ÛÛÛ  Û ° °ÛÛÛ    °°° °ÛÛÛ    °°° 
°ÛÛÛ          °ÛÛÛÛÛÛÛÛÛÛÛ  °ÛÛÛ°°ÛÛÛ °ÛÛÛ  °ÛÛÛÛÛÛ   °°ÛÛÛÛÛÛÛÛÛ °°ÛÛÛÛÛÛÛÛÛ 
°ÛÛÛ    ÛÛÛÛÛ °ÛÛÛ°°°°°ÛÛÛ  °ÛÛÛ °°°  °ÛÛÛ  °ÛÛÛ°°Û    °°°°°°°°ÛÛÛ °°°°°°°°ÛÛÛ
°°ÛÛÛ  °°ÛÛÛ  °ÛÛÛ    °ÛÛÛ  °ÛÛÛ      °ÛÛÛ  °ÛÛÛ °   Û ÛÛÛ    °ÛÛÛ ÛÛÛ    °ÛÛÛ
 °°ÛÛÛÛÛÛÛÛÛ  ÛÛÛÛÛ   ÛÛÛÛÛ ÛÛÛÛÛ     ÛÛÛÛÛ ÛÛÛÛÛÛÛÛÛÛ°°ÛÛÛÛÛÛÛÛÛ °°ÛÛÛÛÛÛÛÛÛ 
   °°°°°°°°°  °°°°°   °°°°° °°°°°     °°°°° °°°°°°°°°°  °°°°°°°°°   °°°°°°°°° 
The syntax to execute GAMESS is
 
   gms.interactive [-l logfile] [-p CPUS] [-w dd:hh:mm:ss] [input]
 
   -l        gives the log file name.
   -p X      will run X compute processes.
   -ppn Y    run only Y compute processes in each node.
   -exepath  full absolute path to the folder containing GAMESS executable
             and rungms.interactive script
   -restart  full absolute path to the restart folder
   -q        partition name passed to SLURM's --partition flag
   -w        wall clock time, as dd:hh:mm:ss (default=24:00:00=24 hrs)
   -mpi      alters rungms.interactive for an MPI job
   -sockets  alters rungms.interactive for an sockets job (default)
   ```

Example:
*  Submit a job using exam01.inp with 1 hr walltime and an MPI build of GAMESS:

   `gms.interactive exam01 -w 1:0:0 -mpi`

Examples:
*  Submit a job using exam01.inp with 1 hr walltime and a sockets build of GAMESS:

   `gms.interactive exam01 -w 1:0:0 -sockets`

   or

   `gms.interactive exam01 -w 1:0:0`

# CyEnce / Condo / Most Linux systems
*  Create a bin folder in your home directory:

   `mkdir $HOME/bin`

*  Add **$HOME/bin** to your path:

   `export PATH=$HOME/bin:$PATH`

*  Copy **gms.interactive** into **$HOME/bin**

*  Copy **rungms.interactive** into **$GMS_DIR** (GAMESS directory)

*  Use the `-exepath` flag to specify the path to the GAMESS directory where the **rungms.interactive** script exists (should be the same path used in the previous step).

   Example:

   `gms.interactive exam01 -w 1:0:0 -mpi -exepath /home/ssok1/dir.git.dev.gamess`

