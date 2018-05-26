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
**Q.**  How do I resolve the following linking error for GAMESS?
```
mkl_semaphore.c:(.text+0x123): undefined reference to `dlopen'
mkl_semaphore.c:(.text+0x152): undefined reference to `dlsym'
...
mkl_memory.c:(.text+0x5b9): undefined reference to `dlopen'
mkl_memory.c:(.text+0x5da): undefined reference to `dlsym'
...
load_library.c:(.text+0x1cd): undefined reference to `dlopen'
load_library.c:(.text+0x1ef): undefined reference to `dlvsym'
...
more undefined references to `dlvsym' follow
```

**A.**  Hardlinking appears to be the issue. You can switch to soft-linking the Intel math library in GAMESS by adding `-so` to the end of the `setenv GMS_MKL_VERNO` line in **install.info**.

For example if the line reads:
```
setenv GMS_MKL_VERNO       12
```

You would change it to:
```
setenv GMS_MKL_VERNO       12-so
```

And re-attempt the linking again with either `lked` or `make`.

----
**Q.** OpenMP sentinels?

**A.**
http://man7.org/linux/man-pages/man1/gfortran.1.html

```
       -fopenacc
           Enable the OpenACC extensions.  This includes OpenACC "!$acc"
           directives in free form and "c$acc", *$acc and "!$acc" directives
           in fixed form, "!$" conditional compilation sentinels in free
           form and "c$", "*$" and "!$" sentinels in fixed form, and when
           linking arranges for the OpenACC runtime library to be linked in.

           Note that this is an experimental feature, incomplete, and
           subject to change in future versions of GCC.  See
           <https://gcc.gnu.org/wiki/OpenACC > for more information.

       -fopenmp
           Enable the OpenMP extensions.  This includes OpenMP "!$omp"
           directives in free form and "c$omp", *$omp and "!$omp" directives
           in fixed form, "!$" conditional compilation sentinels in free
           form and "c$", "*$" and "!$" sentinels in fixed form, and when
           linking arranges for the OpenMP runtime library to be linked in.
           The option -fopenmp implies -frecursive.
```
----
**Q.** Why am I getting inaccurate results for LIBCCHEM runs using LIBINT?

**A.** The issue is tied to the renormalization.  
*  Comment out `//renorm()` on **line 129** in `libint/include/libtin2/shell.h`
*  Inside the `libcchem` folder run:
   *  `make && make install`
*  Inside the `$GMS_DIR` folder run:
   *  `make`
*  Try the libcchem run again.
----
**Q.** I get the following error: `semget errno=ENOSPC -- check system limit for sysv semaphores.`

**A.** Increase the semaphore limits for the max number of arrays.

You can check the current limit by issuing:

`ipcs -l`

You can change the limits (as sudo or root by doing) replacing:

```
MAX_SEMAPHORE_PER_ARRAY_VALUE
MAX_SEMAPHORE_SYSTEM_WIDE
MAX_OPS_PER_SEMO_CALL
MAX_NUMBER_OF_ARRAYS
```

below with the numeric values you desire.

`printf 'MAX_SEMAPHORE_PER_ARRAY_VALUE\tMAX_SEMAPHORE_SYSTEM_WIDE\tMAX_OPS_PER_SEMO_CALL\tMAX_NUMBER_OF_ARRAYS' >/proc/sys/kernel/sem`

In this case increasing the value for `MAX_NUMBER_OF_ARRAYS`.
