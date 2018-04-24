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



