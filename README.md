# Frequently Asked Questions

Feel free to edit this repository with questions and answers. I encourage the use of [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

Resources for CyEnce/SLURM

*  [Iowa State HPC Guide](https://www.hpc.iastate.edu/guides)
*  [SLURM @ Iowa State](https://www.hpc.iastate.edu/sites/default/files/uploads/HPCHowTo/2018%20April%2011%20How%20to%20Use%20Condo-CyEnce.pdf )

----

**Q.**  I don’t know if we can set up a page of “frequently asked question” for GAMESS. I have posted a bunch of questions on Slack. Though all questions have been answered with very nice instructions, it can be difficult to trace back these questions and instructions after a while.

**A.**  This repository.

----

**Q.**  I think scripts in GAMESS (comp, compall, lked, config, rungms and gms) are very powerful by covering a variety number of machines, communications, compilers; but it’s difficult to navigate and modify these scripts. I don’t know if we can make templates with minimum information to compile, link and run jobs using these scripts.

**A.**  The `config` script exists to remove the need to modify `comp`, `compall`, and `lked` - which makes use of the `install.info` file that is generated from the `config` process.  You should not need to make any modifications to `comp`, `compall`, and `lked` unless you are adding a new target, compiler, math library, or communication library.

   An alternative to `rungms` is the `rungms.interactive` script that can be found in **$GMS_DIR/machines/xeon-phi/**. Copy it to your $GMS_DIR folder. The script is initially setup for `mpi` but if you need `sockets` or `ga` then you will need to change:

`set TARGET=mpi`

within the rungms.interactive script.

An alternative to `config` makes use of Python3 and Jinja2 templating. Have a look at the following [branch](https://github.com/gms-bbg/gamess/tree/saromleang/jinja-templating). Execute:

`./bin/create-install-info.py --help`

to see usage information.  The script will generate an `install.info`, compile `actvte.x`, and produce a `rungms` script based off `install.info`.

The `gms` script is specialized for a given cluster and queuing system. There is no simple template for this file.

----

**Q.**  Which fortran extension should be used? How does the fortran extension affect OpenMP?

**A.**  A good example: https://software.intel.com/en-us/node/677900

----
