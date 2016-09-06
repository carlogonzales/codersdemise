# Hadoop HDFS "No Such File or Directory" on `ls`

After a fresh setup and installation of hadoop then when you run `hdfs dfs -ls` and recieved an `ls: '.': No such file or directory` instead of a directory listing; you probably missed creating your user's home folder. The default base folder everytime you use any relative paths or implicitly indicating a directory parameter, always resolves to your home folder. By default this folder's non-existent and should be created after a fresh installation. To set it up, you only have to manually create the directory for your user.

#### Step 1

Create the directory tree.

```bash
hdfs dfs -mkdir -p /user/hdfsuser
```

#### Step 2

Validate the creation of the folder by reentering `hdfs dfs -ls`.
