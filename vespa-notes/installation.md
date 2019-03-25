# Installing VESPA and vespa-slim



## Installing VESPA

- Download [`vespa_conda.yml`](vespa_conda.yml)
- run `conda env create -f vespa_conda.yml`
- This will install some but not all of the binary dependencies
  - (and a load of other unused dependencies Andrew put in the conda env)
    - Don't put it in your base environment...



## Installing vespa-slim

- Create a new Python 3.6+ virtualenv or conda env and pip(3) install
- Download latest tarball from github, decompress and run
  - `pip install /path/to/vespa-slim-master`