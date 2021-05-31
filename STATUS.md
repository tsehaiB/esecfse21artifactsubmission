# Status

We are applying for the "Artifacts Evaluated - Reusable" and the
"Artifacts Available" badges.  Please see the discussion below for our
rationale.

## Artifact Evaluated - Reusable

We believe the [artifact](https://zenodo.org/record/4885001) is
reusable because it significantly exceeds the functional requirement.

- Documented: the artifact contains detailed requirements,
  installation, and usage instructions.

- Consistent: the artifact contains script to replicate the results
  found in the paper.

- Complete: the artifact includes all source code, scripts, and usage
  instructions for using the resulting artifact and repeating the
  experiments.  The resulting
  [data](https://zenodo.org/record/4563310) are also archived.

- Exercisable: the artifact includes installation instructions,
  commands, and scripts for using the tooling and repeating the
  experiments.

- Exceeds functional: the artifact exceeds functional in several ways:
  - The tooling uses best practices for packaging and distributing
    software, using Python's disttools as well as the PyPI package
    index.
  - The tooling is self-documented, with each component containing
    detailed instructions for each command via the `-h` flag.
  - The infrastructure contains several components, `kismet`,
    `kclause`, `kextract`, `klocalizer`, that each stand on their own
    as reusable command-line tools.
  - The individual components can be repurposed in future
    applications, since they have well-defined, well-documented
    interfaces and file formats.
  - System requirements are well-documented, with only a few commands
    to run to set them up.
  - Installation is simple, requiring only a single command to install.
  - The repetition scripts are fully automated, requiring no
    additional manual steps to repeat the paper's experiments.

## Artifacts Available

This artifact and its resulting data are both archived publicly on
Zenodo.  This artifact has DOI
[10.5281/zenodo.4883930](https://zenodo.org/record/4885001).  The
resulting data has DOI
[10.5281/zenodo.4563310](https://zenodo.org/record/4563310).
