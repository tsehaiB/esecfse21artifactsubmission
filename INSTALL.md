# Installation instructions

## Obtain the artifact

Download and unzip the artifact:

    wget https://zenodo.org/record/4885001/files/esecfse21artifact.zip
    unzip esecfse21artifact.zip

## (Optional but recommended) Prepare a virtual machine with vagrant

The artifact has been evaluated on Ubuntu 20.04 and should work on
Debian-based GNU/Linux distributions.  If using another system or
version, or if an isolated environment is preferred, prepare a virtual
machine to install the artifact.  These instructions use the
[vagrant](https://www.virtualbox.org/wiki/Downloads) tool to manage a
[VirtualBox](https://www.vagrantup.com/downloads) virtual machine, but
an [Ubuntu 20.04](http://www.releases.ubuntu.com/20.04/) ISO can also
be installed by hand on VirtualBox or with any other virtualization
platform.  This step is not necessary if a native installation with
the tested version is available.

Install vagrant and VirtualBox:

- Install [VirtualBox](https://www.vagrantup.com/downloads) (tested on v6.1.16)

- Install [vagrant](https://www.virtualbox.org/wiki/Downloads) (tested on v2.2.6)

(Note: each vagrant version has compatibility with only specific
VirtualBox versions.)

Create the virtual machine:

    cd esecfse21artifact/
    vagrant up

This will take a couple of minutes to download and boot the VM
image.

Enter the virtual machine:

    vagrant ssh

The prompt should be `vagrant@ubuntu-groovy:~$ `

## Prepare system dependencies

Assuming an Ubuntu 20.04 (or other Debian-based) installation, the
following instructions will install dependencies. For more information on the individual dependencies, click the corresponding hyperlinks. 

<big><pre>
sudo apt update
sudo apt install -y [python3-pip](https://www.w3schools.com/python/python_pip.asp) [python3-venv](https://realpython.com/python-virtual-environments-a-primer/) [flex](http://web.mit.edu/gnu/doc/html/flex_1.html#:~:text=flex%20is%20a%20tool%20for,and%20C%20code%2C%20called%20rules%20.) [bison](https://www.gnu.org/software/bison/#:~:text=Bison%20is%20a%20general%2Dpurpose,LALR%20(1)%20parser%20tables.&text=Anyone%20familiar%20with%20Yacc%20should,use%20Bison%20with%20little%20trouble.) [bc](https://linux.die.net/man/1/bc) [libssl-dev](https://cygwin.com/packages/summary/libssl-devel.html) [libelf-dev](https://yum-info.contradodigital.com/view-package/base/elfutils-libelf-devel/)
</pre></big>

## Install the kclause/kismet software

We will install the software into a python virtual environment.  While
this is optional, it will ensure isolation from your system python
installation:

    python3 -m venv kmax_env  # create the environment
    source kmax_env/bin/activate  # enter the environment

Install from the source distributed with the artifact package.  (If
running natively without the Vagrant virtual machine, then replace
`/vagrant/kmax` with the path to the artifact package, i.e.,
`PATH_TO_ARTIFACT/kmax`.)

    (cd /vagrant/kmax && python3 setup.py install)

Up-to-date source with installation instructions can also be found in
the [repository](https://github.com/paulgazz/kmax#getting-started).

If there are installation issues, try using the vagrant virtual
machine option, since this installation path has the least variance
from the tested artifact.

## Kicking the tires

Get a copy of the Linux source code (already available on the pre-installed virtual machine)

    wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.4.4.tar.xz
    tar -xvf linux-5.4.4.tar.xz
        
Enter the source directory

    cd linux-5.4.4/

Run the `klocalizer` component as a test.  This will take 2-3 minutes
with a native installation on a commodity.

    klocalizer drivers/usb/storage/alauda.o

The output should look like this, with the last line being `x86_64`
denoting the successful creation of a `.config` file for the `x86_64`
architecture.

    WARNING: No cached formulas for 5.4.4 available for download :(
    INFO: Trying the following architectures: x86_64 i386 arm arm64 sparc64 sparc powerpc mips alpha arc c6x csky h8300 hexagon ia64 m68k microblaze nds32 nios2 openrisc parisc riscv s390 sh sh64 um unicore32 xtensa
    INFO: Trying "x86_64"
    [STEP 1/3] reading kextract file
    [STEP 1/3] finished reading kextract file
    [STEP 2/3] translated 14254/14254 configuration option dependencies
    [STEP 3/3] converted 14197/14197 constraints to smtlib2 format
    [STEP 3/3] pickling the map
    [STEP 3/3] done
    INFO: The constraints are satisfiable.
    INFO: Writing the configuration to .config
    INFO: Build with "make.cross ARCH=x86_64 olddefconfig; make.cross ARCH=x86_64 clean drivers/usb/storage/alauda.o".
    x86_64

Please see the [README.md](./README.md) for instructions on repeating the paper's experiments.
