# Cluster notes



### Use entire 24 core, 128GB Leeds 'Omics node for up to 48hrs

```Shell
#$ -P omics
#$ -l h_rt=48:00:00
#$ -l nodes=1,ppn=24
```





### Execute a file of newline separated commands as a task array

```shell
#$ -t 1-42
CMD=$(awk "NR==$SGE_TASK_ID" cmds.txt)
eval $CMD
```

(e.g. where `cmds.txt` has 42 commands each separated by a newline)





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

