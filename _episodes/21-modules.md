---
title: "Accessing software and packages"
teaching: 30
exercises: 15
questions:
- "How do we load and unload software packages?"
objectives:
- "Understand how to load and use a software package."
keypoints:
- "Load software with `module load softwareName`"
- "Unload software with `module purge`"
- "The module system handles software versioning and package conflicts for you automatically."
- "You can edit your `.bashrc` file to automatically load a software package."
---

By default, no software is loaded onto your work space.
If we want to use a software or package, we will need to "load" it ourselves.

Before we start using individual software packages, however, 
we should understand the reasoning behind this approach.
The two biggest factors are software incompatibilities and versioning.

Software incompatibility is a major headache for programmers.
Sometimes the presence (or absence) 
of a software package will break others that depend on it.
Two of the most famous examples are Python 2 and 3 and C compiler versions.
Python 3 famously provides a `python` command 
that conflicts with that provided by Python 2. 
Software compiled against a newer version of the C libraries 
and then used when they are not present will result in a nasty
`'GLIBCXX_3.4.20' not found` error, for instance. 

Software versioning is another common issue.
A team might depend on a certain package version for their research project - 
if the software version was to change (for instance, if a package was updated),
it might affect their results.
Having access to multiple software versions allow a set of researchers to take 
software version out of the equation if results are weird.

## Environment modules (Lmod)

Environment modules are the solution to these problems.
A module is a self-contained software package - 
it contains all of the files required to run a software packace 
and loads required dependencies.

To see available software modules, use `module availiable`
If the module you require is not avaliable on the HPC then fill in <a href="https://forms.office.com/Pages/ResponsePage.aspx?id=q8h8Wtykm0-_YGZxQEmtYhZRHEbGuutOhsLljzWVJ1JUQlRTM0lTV0o0TFozWjlVMTQ5TVU0WjhBSC4u" target="_blank">this form</a> and in "Problem Description" write the software/package you would like along with the version number.

```
module availiable
```
{: .bash}
```
--------------------------------- /usr/share/Modules/modulefiles ---------------------------------
dot         module-git  module-info modules     null        use.own

---------------------------------------- /etc/modulefiles ----------------------------------------
mpi/mpich-3.2-x86_64

------------------------------------------ /sw/Modules -------------------------------------------
anaconda2/2019.07py2                      library/hdf5/5-1.10.5-intel
anaconda3/2019.07py3                      library/lapack/3.8.0
ansys/v195                                library/loki/0.1.7
bioinformatics/blast+/2.9.0               library/netcdf/netcdf-c/4.7.3
bioinformatics/bowtie2/2.3.5.1            library/netcdf/netcdf-c/4.7.3-intel
bioinformatics/cd-hit/4.8.1               library/netcdf/netcdf-cxx/4.3.1
bioinformatics/celSEQpipeline/1.0         library/netcdf/netcdf-cxx/4.3.1-intel
bioinformatics/fastqc/0.11.8              library/netcdf/netcdf-fortran/4.5.2
bioinformatics/htslib/1.9                 library/netcdf/netcdf-fortran/4.5.2-intel
bioinformatics/orthofinder/2.3.7          library/openblas/0.3.6
bioinformatics/samtools/1.9               library/proj/6.2.1
bioinformatics/signalp/4.1                library/scalapack/2.0.2
bioinformatics/tmhmm/2.0                  library/tcl/8.6.9
bioinformatics/transdecoder/5.5.0         library/tk/8.6.9
bioinformatics/trinity/2.8.6              library/vtk/8.2.0
cmake/3.15.5                              library/xz/5.2.4
cmake/3.8.2                               matlab/2018b
delft3d/6244intel                         matlab/2019b
extras/jags/4.3.0                         misc/aem3d/1.0.1
gaussian/g16                              misc/aem3d/aem3d
gcc/8.3.1                                 misc/automake/1.15
gcc/old/9.2.0                             misc/baronsolver/19.7.13
gcc/old/9.2.0OLD                          misc/cplex/cplex
gromacs/2019.3                            misc/libtool/2.4.6
gromacs/2019.4                            misc/metashape/1.5.2
gromos/md++141                            misc/metashape/1.5.3pro
intel/ics2013                             misc/metis/5.1.0
intel/intelmpi                            misc/qglviewer/2.6.3
intel/intelParallelStudio2019             misc/qglviewer/2.7.1
java/jdk11.0.1                            misc/simbody/361
lang/golang/1.21.0                        misc/yade/2019.01a
lang/golangci-lint/1.21.0                 misc/yasara/yasara
legacy/gcc/4.9.3                          mpi/mpich/3.3.2-gnu
library/boost/1.59.0py3                   mpi/mpich/3.3.2-intel
library/boost/1.70.0py2                   mpi/openmpi/2.1.6
library/boost/1.70.0py3                   mpi/openmpi/4.0.2
library/cgal/4.13.1                       python/2.7.17
library/eigen/3.3.7                       python/3.7.4
library/fftw/3.3.8                        qt/5.12.3
library/fftw/3.3.8mpi                     quantum-espresso/6.4.1
library/gdal/3.0.2                        R/3.6.1
library/geos/3.8.0                        singularity/3.2.0
library/gts/0.7.6                         vasp/vasp541-gnu-openmpi
library/hdf4/4.2.13                       virtualgl/2.6.3
library/hdf5/5-1.10.5
```
{: .output}

## Loading and unloading software

To load a software module, use `module load`.
In this example we will use R. We can see that version of R is 3.6.1

Intially, R is not loaded. 

```
which R
```
{: .bash}
```
no R in (/opt/clmgr/sbin:/opt/clmgr/bin:/opt/sgi/sbin:/opt/sgi/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/c3/bin:/opt/pbs/bin:/sbin:/bin:/export/home/sNumber/bin)
```
{: .output}

We can load R using the command `module load`.

```
module load R
R --version
```
{: .bash}
```
R version 3.6.1 (2019-07-05) -- "Action of the Toes"
Copyright (C) 2019 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```
{: .output}

What if we want a specific version. There is only 1 version of R avaliable to the HPC, remember the command `module avaliable`. There are 2 versions of matlab avaliable though, 2018b and 2019b. Lets load matlab/2019b.

```
module load matlab/2019b
matlab --version
```
{: .bash}
```

So what just happened?

To understand the output, first we need to understand the nature of the 
`$PATH` environment variable.
`$PATH` is a special ennvironment variable that controls where a UNIX system looks for software.
Specifically `$PATH` is a list of directories (separated by `:`)
that the OS searches through for a command before giving up and telling us it can't find it.
As with all environment variables we can print it out using `echo`.

```
echo $PATH
```
{: .bash}
```
-bash: /sw/python/3.7.4/bin:/opt/clmgr/sbin:/opt/clmgr/bin:/opt/sgi/sbin:/opt/sgi/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/opt/c3/bin:/opt/pbs/bin:/sbin:/bin:/export/home/sNumber/bin: No such file or directory
```
{: .output}

You'll notice a similarity to the output of the `which` command. 
In this case, there's only one difference:
the `/sw/python/3.7.4/bin` directory at the beginning.
When we ran `module load ; which python3`, 
it added this directory to the beginning of our `$PATH`.
Let's examine what's there:

```
ls /sw/python/3.7.4/bin
```
{: .bash}
```
2to3                                                export-workflow               ptrepack
2to3-3.7                                            f2py                          pttree
bc_demultiplex                                      f2py3                         pydoc3
celseq2                                             f2py3.7                       pydoc3.7
celseq2-diagnose                                    futurize                      pytest
celseq2-dummy-species                               geo_generate_sample_sheet.py  py.test
celseq2-qc                                          htseq-count                   python
celseq2-simulate                                    htseq-qa                      python3
celseq2-slim                                        idle3                         python3.7
celseq2-test                                        idle3.7                       python3.7-config
celseq2-to-st                                       jsonschema                    python3.7m
chardetect                                          jupyter                       python3.7m-config
cook-annotation                                     jupyter-migrate               python3-config
count-umi                                           jupyter-troubleshoot          pyvenv
cygdb                                               jupyter-trust                 pyvenv-3.7
cython                                              ncbi_extract_entrez2gene.py   rnaseq_stringtie_gene_level_expression.py
cythonize                                           new-configuration-file        sam-demultiplex
easy_install                                        new-experiment-table          seq_trim_fastq.py
easy_install-3.7                                    pasteurize                    snakemake
ensembl_extract_protein_coding_exon_annotations.py  pip                           snakemake-bash-completion
ensembl_extract_protein_coding_gene_ids.py          pip3                          sra_find_experiment_runs.py
ensembl_extract_protein_coding_genes.py             pip3.7                        virtualenv
ensembl_filter_fasta.py                             pt2to3                        wheel
exp_convert_entrez2gene.py                          ptdump

```
{: .output}

Taking this to it's conclusion, `module load` will add software to your `$PATH`.
It "loads" software.
A special note on this - 
depending on which version of the `module` program that is installed at your site,
`module load` will also load required software dependencies.
To demonstrate, let's use `module list`.
`module list` shows all loaded software modules.

```
module list
```
{: .bash}
```
Currently Loaded Modulefiles:
  1) python/3.7.4
```
{: .output}

```
module load R
module list
```
{: .bash}
```
Currently Loaded Modulefiles:
  1) python/3.7.4   2) R/3.6.1
```
{: .output}

So in this case, the software `R` was loaded into you HPC workspace.
Let's try unloading the `R` software.

```
module unload R
module list
```
{: .bash}
```
Currently Loaded Modulefiles:
  1) python/3.7.4
```
{: .output}

So using `module unload` "un-loads" a module along with it's dependencies.
If we wanted to unload everything at once, we could run `module purge` (unloads everything).

```
module purge
```
{: .bash}
```
No Modulefiles Currently Loaded.
```
{: .output}

Note that `module purge` is informative. 
It lets us know that all but a default set of packages have been unloaded
(and how to actually unload these if we truly so desired).

## Software versioning

So far, we've learned how to load and unload software packages.
This is very useful.
However, we have not yet addressed the issue of software versioning.
At some point or other, 
you will run into issues where only one particular version of some software will be suitable.
Perhaps a key bugfix only happened in a certain version, 
or version X broke compatibility with a file format you use.
In either of these example cases, 
it helps to be very specific about what software is loaded.

Let's examine the output of `module availiable` more closely.

```
module availiable
```
{: .bash}
```
--------------------------------- /usr/share/Modules/modulefiles ---------------------------------
dot         module-git  module-info modules     null        use.own

---------------------------------------- /etc/modulefiles ----------------------------------------
mpi/mpich-3.2-x86_64

------------------------------------------ /sw/Modules -------------------------------------------
anaconda2/2019.07py2                      library/hdf5/5-1.10.5-intel
anaconda3/2019.07py3                      library/lapack/3.8.0
ansys/v195                                library/loki/0.1.7
bioinformatics/blast+/2.9.0               library/netcdf/netcdf-c/4.7.3
bioinformatics/bowtie2/2.3.5.1            library/netcdf/netcdf-c/4.7.3-intel
bioinformatics/cd-hit/4.8.1               library/netcdf/netcdf-cxx/4.3.1
bioinformatics/celSEQpipeline/1.0         library/netcdf/netcdf-cxx/4.3.1-intel
bioinformatics/fastqc/0.11.8              library/netcdf/netcdf-fortran/4.5.2
bioinformatics/htslib/1.9                 library/netcdf/netcdf-fortran/4.5.2-intel
bioinformatics/orthofinder/2.3.7          library/openblas/0.3.6
bioinformatics/samtools/1.9               library/proj/6.2.1
bioinformatics/signalp/4.1                library/scalapack/2.0.2
bioinformatics/tmhmm/2.0                  library/tcl/8.6.9
bioinformatics/transdecoder/5.5.0         library/tk/8.6.9
bioinformatics/trinity/2.8.6              library/vtk/8.2.0
cmake/3.15.5                              library/xz/5.2.4
cmake/3.8.2                               matlab/2018b
delft3d/6244intel                         matlab/2019b
extras/jags/4.3.0                         misc/aem3d/1.0.1
gaussian/g16                              misc/aem3d/aem3d
gcc/8.3.1                                 misc/automake/1.15
gcc/old/9.2.0                             misc/baronsolver/19.7.13
gcc/old/9.2.0OLD                          misc/cplex/cplex
gromacs/2019.3                            misc/libtool/2.4.6
gromacs/2019.4                            misc/metashape/1.5.2
gromos/md++141                            misc/metashape/1.5.3pro
intel/ics2013                             misc/metis/5.1.0
intel/intelmpi                            misc/qglviewer/2.6.3
intel/intelParallelStudio2019             misc/qglviewer/2.7.1
java/jdk11.0.1                            misc/simbody/361
lang/golang/1.21.0                        misc/yade/2019.01a
lang/golangci-lint/1.21.0                 misc/yasara/yasara
legacy/gcc/4.9.3                          mpi/mpich/3.3.2-gnu
library/boost/1.59.0py3                   mpi/mpich/3.3.2-intel
library/boost/1.70.0py2                   mpi/openmpi/2.1.6
library/boost/1.70.0py3                   mpi/openmpi/4.0.2
library/cgal/4.13.1                       python/2.7.17
library/eigen/3.3.7                       python/3.7.4
library/fftw/3.3.8                        qt/5.12.3
library/fftw/3.3.8mpi                     quantum-espresso/6.4.1
library/gdal/3.0.2                        R/3.6.1
library/geos/3.8.0                        singularity/3.2.0
library/gts/0.7.6                         vasp/vasp541-gnu-openmpi
library/hdf4/4.2.13                       virtualgl/2.6.3
library/hdf5/5-1.10.5
```
{: .output}

Let's take a closer look at the `gcc` module.
GCC is an extremely widely used C/C++/Fortran compiler.
Tons of software is dependent on the GCC version, 
and might not compile or run if the wrong version is loaded.
In this case, there are two different versions: `gcc/8.3.1`, `gcc/old/9.2.0` and `gcc/old/9.2.0OLD`.
How do we load each copy and which copy is the default?

```
module load gcc
gcc --version
```
{: .bash}
```
gcc (GCC) 9.2.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
{: .output}


Note that three things happened:
the default copy of GCC was loaded (version 5.4.0), 
the Intel compilers (which conflict with GCC) were unloaded,
and software that is dependent on compiler (OpenMPI) was reloaded.
The `module` system turned what might be a super-complex operation into a single command.

So how do we load the non-default copy of a software package?
In this case, the only change we need to make is be more specific about the module we are loading.
There are two GCC modules: `gcc/5.4.0` and `gcc/4.8.5`.
To load a non-default module, the only change we need to make to our `module load` command
is to leave in the version number after the `/`.

```
module load gcc/4.8.5
gcc --version
```
{: .bash}
```
Inactive Modules:
  1) openmpi

The following have been reloaded with a version change:
  1) gcc/5.4.0 => gcc/4.8.5

gcc (GCC) 4.8.5
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
{: .output}

We now have successfully switched from GCC 5.4.0 to GCC 4.8.5.
It is also important to note that there was no compatible OpenMPI module available for GCC 4.8.5.
Because of this, the `module` program has "inactivated" the module.
All this means for us is that if we re-load GCC 5.4.0, 
`module` will remember OpenMPI used to be loaded and load that module as well.

```
module load gcc/5.4.0
```
{: .bash}
```
Activating Modules:
  1) openmpi/2.1.1

The following have been reloaded with a version change:
  1) gcc/4.8.5 => gcc/5.4.0
```
{: .output}

> ## Using software modules in scripts
>
> Create a job that is able to run `python3 --version`.
> Remember, no software is loaded by default!
> Running a job is just like logging on to the system 
> (you should not assume a module loaded on the login node is loaded on a worker node).
{: .challenge}

> ## Loading a module by default
> 
> Adding a set of `module load` commands to all of your scripts and
> having to manually load modules every time you log on can be tiresome.
> Fortunately, there is a way of specifying a set of "default modules"
> that always get loaded, regardless of whether or not you're logged on or running a job.
>
> Every user has two hidden files in their home directory: `.bashrc` and `.bash_profile`
> (you can see these files with `ls -la ~`).
> These scripts are run every time you log on or run a job.
> Adding a `module load` command to one of these shell scripts means that
> that module will always be loaded.
> Modify either your `.bashrc` or `.bash_profile` scripts to load a commonly used module like Python.
> Does your `python3 --version` job from before still need `module load` to run?
{: .challenge}


So here we loaded the required modules using the command line, however we don't want to do this each time we run our analysis. As seen in the previous section we can load modules with the scheduler script.