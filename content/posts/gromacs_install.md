---
title: "Installing GROMACS on the UC Davis FARM cluster: or install GROMACS without sudo privileges."
date: 2020-12-30
tags: ['programming', 'blogs', 'guides']
draft: false
---

Are you using the UC Davis [FARM](https://wiki.cse.ucdavis.edu/support/systems/farm) 
for molecular modeling and need to figure out
how to setup [GROMACS](http://www.gromacs.org/)? Well hello extremely small subset
of the population! This is the guide for you. 

Note, this is only for a basic installation. For maximum performance refer to the
GROMACS guide linked above. 

## Getting started

We will be working off the installation instructions on the 
[GROMACS website](http://www.gromacs.org/Documentation_of_outdated_versions/Installation_Instructions_5.0#TOC)
but will modify a few steps to deal with the quirks of the FARM at the time
of writing and the fact you will not have `sudo` privileges. 

If you want to cut to the chase, you can [run this script](/posts/code/farm_install_gromacs.sh), which will
run all the code in this guide in one go. Everything will be downloaded / complied
in the directory you run the script in. You can use the command below to download
the script, give it permission to run, and then run it. 

```bash
wget http://ethanholleman.github.io/posts/code/farm_install_gromacs.sh; chmod 777 farm_install_gromacs.sh; ./farm_install_gromacs.sh
```

With that in mind the first thing to do is select a directory where you will
download everything, `cd` into it and get going.

## Download and install a recent `cmake` version 

At the time of writing, the FARM is running `cmake 3.10.2` while GROMACS requires
at least `3.13.0` to build. I will be downloading `3.19.2` as it is the most
recent at the time of writing. If you are downloading a different version
you will have to modify some of the commands to reflect that (this will be
true for all downloaded programs).

Download and run the install with the commands below

```bash
wget https://github.com/Kitware/CMake/releases/download/v3.19.2/cmake-3.19.2-Linux-x86_64.sh
chmod 777 cmake-3.19.2-Linux-x86_64.sh
echo "Running cmake installer"
./cmake-3.19.2-Linux-x86_64.sh
```

## Download and compile GROMACS

Download your preferred version of GROMACS from [the docs](https://manual.gromacs.org/),
I will be using `2021-rc1` for this guide.

```bash
wget http://ftp.gromacs.org/pub/gromacs/gromacs-2021-rc1.tar.gz 
tar xfz gromacs-2021-rc1.tar.gz
```

Now enter into the newly downloaded GROMACS directory and create a build directory. 

```bash
cd gromacs-2021-rc1
mkdir build
cd build
```

From the build directory run the newly downloaded `cmake` version by determinging
the path to the `cmake` exe. It will be located in folder produced by the `cmake`
installer. For me, the full path was 
`/home/ethollem/software/cmake-3.19.2-Linux-x86_64/cmake-3.19.2-Linux-x86_64/bin/cmake`.

Then run `cmake` with your version subsituted into `[cmake]` below.

```bash
[cmake] .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=ON
```

Then make the program (this could take a while).

```bash
make
make check
```

The GROMACS guide recommends the following command

```bash
sudo make install
```

but since we do not have sudo privileges to run the program we can add the
exe to out PATH variable. From the
build directory the GROMACS exe path will be `[Your absolute path to build dir]/bin/gmx`.
For me this looks like `home/ethollem/software/gromacs-2021-rc1/build/bin/gmx`.

Open / create `~/.bashrc` using your preferred text editor and add the line

```bash
export PATH="$HOME/software/gromacs-2021-rc1/build/bin/gmx:$PATH"
```

Then log off and log back in again. Test everything is working correctly by running
```bash
gmx --help
```

You should be greeted wih the GROMACS help page. If you are you are now good
to go.