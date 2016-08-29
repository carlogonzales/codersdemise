# Hadoop HDFS "No Such File or Directory" on `ls`

After a fresh setup and installation of hadoop then when you run `hdfs dfs -ls` and recieved an `ls: '.': No such file or directory` instead of a directory listing. You most likely forgot to create the home directory for your user. To set it up, you only have to manually create the directory for your user.

#### Step 1

Create the directory tree.

```bash
hdfs dfs -mkdir -p /user/hdfsuser
```

#### Step 2

Validate the creation of the folder by reentering `hdfs dfs -ls`.
