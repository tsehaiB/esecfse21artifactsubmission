# Artifact overview

This is the artifact for "Finding Broken Linux Configuration
Specifications by Statically Analyzing the Kconfig Language" by Jeho
Oh, Necip Fazıl Yıldıran, Julian Braha, and Paul Gazzillo to appear at
the 2021 European Software Engineering Conference and ACM SIGSOFT
Symposium on the Foundations of Software Engineering (ESEC/FSE).

A snapshot of the complete public repository can be found in the
[vagrant/kmax/](vagrant/kmax/) folder included in this artifact.  So
any links to files in https://github.com/paulgazz/kmax can also be
found in their corresponding path in [vagrant/kmax/](vagrant/kmax/).

## Obtaining the artifact

The artifact can be obtained from its [Zenodo
archive](https://zenodo.org/record/4885001), while up-to-date source
is also available from the [git
repository](https://github.com/paulgazz/kmax).

Please see [INSTALL.md](./INSTALL.md) for detailed installation
instructions

## Repeating the experiment

(These instructions assume the installation is already complete, as
described in [INSTALL.md](./INSTALL.md)).

The full experiment can take about 20 hours on commodity desktop
hardware but, being embarrassingly parallel, each of the Linux source
code's supported architectures can be run separately and
independently.  For instance, running `kismet` on just the `x86_64`
specifications takes about 45 minutes on commodity hardware.  The
following instructions show both `kismet` on just the `x86_64` kernel
configuration specifications as well as the commands for the [full
experiment](https://github.com/paulgazz/kmax/blob/master/scripts/kismet_experiments_replication.sh).

### `x86_64` configuration specifications only

Get linux 5.4.4 source

    mkdir -p ~/kismet-experiments/
    cd ~/kismet-experiments
    wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.4.4.tar.xz
    tar -xvf linux-5.4.4.tar.xz

Run `kismet`

    kismet --linux-ksrc="linux-5.4.4/" -a=x86_64 --test-cases-dir="test_cases_x86_64/"

The resulting alarms can be found in `kismet_summary_x86_64.csv` and
summary of the experiment in `kismet_summary_x86_64.txt`.

### Full repetition

(This script also can be found in the [source
repository](https://github.com/paulgazz/kmax/blob/master/scripts/kismet_experiments_replication.sh).)

    #!/bin/bash

    set -x

    which kismet

    # get linux 5.4.4 source
    mkdir -p ~/kismet-experiments/
    cd ~/kismet-experiments
    wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.4.4.tar.xz
    tar -xvf linux-5.4.4.tar.xz

    # todo: um32 is not supported by kextract, add it once resolved
    ARCHS=("x86_64" "i386" "arm" "arm64" "sparc64" "sparc" "powerpc" "mips" "alpha" "arc" "c6x" "csky" "h8300" "hexagon" "ia64" "m68k" "microblaze" "nds32" "nios2" "openrisc" "parisc" "riscv" "s390" "sh" "sh64" "um" "unicore32"  "xtensa")

    for arch in ${ARCHS[@]}; do
      echo "running kismet on ${arch}"
      /usr/bin/time -o script_time_${arch}.txt kismet --linux-ksrc="linux-5.4.4/" -a=${arch} --test-cases-dir="test_cases_${arch}/" > script_log_${arch}.txt 2>&1
      echo "kismet done running on ${arch}"
    done

The resulting alarms can be found in `kismet_summary_ARCH.csv` and
summary of the experiment in `kismet_summary_ARCH.txt`.
