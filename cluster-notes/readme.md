# Cluster notes

### Use ARC3 high memory nodes

```shell
#$ -l node_type=24core-768G
```

### Use entire 24 core, 128GB Leeds 'Omics node for up to 48hrs

```Shell
#$ -P omics
#$ -l h_rt=48:00:00
#$ -l nodes=1,ppn=24
```

---


### Execute a file of newline separated commands as a task array

```shell
#$ -t 1-42
CMD=$(awk "NR==$SGE_TASK_ID" cmds.txt)
eval $CMD
```

(e.g. where `cmds.txt` has 42 commands each separated by a newline)

---

### Prevent periodic ARC3 `/nobackup` file deletion

- Create a file named `.not_expire.sh ` in your **home directory**

- Edit the file to contain the following:

- ```shell
  cd /nobackup/your_directory_name
  find . -print0 | xargs -0 touch -h
  ```

- Open the crontab in the currently defined editor
  `$ crontab -e`

- Edit the first line to read:

  `0 4 4 * * ~/.not_expire.sh`

---

### Example job script

```shell
#$ -cwd                                                                        
#$ -V                                                                          
#$ -P omics
#$ -l h_rt=48:00:00                                                              
#$ -l h_vmem=16G
#$ -t 1-57936
#$ -tc 150

CMD=$(awk "NR==$SGE_TASK_ID" codeml/codeml_commands.sh)
eval $CMD
```

---

### Install and run vespa-slim

Some day you'll be able to pip install `vespa-slim` but until then you'll need to dowload the tarball from the [GitHub repo](https://github.com/bede/vespa-slim). If you can't see, ask Bede for access.

**Install**

```shell
$ module load python/3.6.5  # Or some other version of Python 3
$ tar -xzf vespa-slim.tar.gz
$ pip install --user vespa-slim/
```
**Run**

```shell
$ module load python/3.6.5  # Or some other version of Python 3
$ vespa -h
usage: vespa [-h] {infer-gene-trees,codeml-setup} ...

positional arguments:
  {infer-gene-trees,codeml-setup}
    infer-gene-trees    Create gene trees by pruning a given species tree
    codeml-setup        Create suite of branch and branch-site codeml
                        environments

optional arguments:
  -h, --help            show this help message and exit

$ vespa infer-gene-trees -h
usage: vespa infer-gene-trees [-h] [-o OUTPUT] [-s SEPARATOR] [-p] input tree

Create gene trees by pruning a given species tree

positional arguments:
  input                 path to directory containing gene families
  tree                  path to newick formatted species tree

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        path to output directory (default: 'gene-trees')
  -s SEPARATOR, --separator SEPARATOR
                        character separating taxon name and identifier(s)
                        (default: '|')
  -p, --progress        show progress bar (default: False)
```

