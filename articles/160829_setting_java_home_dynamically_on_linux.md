# Setting JAVA_HOME Dynamically on Linux

There are two flavor of JDK you can get from any Linux ditros, OpenJDK or from Oracle. These software can be installed manually, assigning the static path on JAVA_HOME. What if you installed it directly from `yum` or `apt`, how can you assign the correct Java directory for a managed installation?

_Note: This how-to assumes you're using `bash` as your shell. Feel free to apply it based on what shell you're using._

### User Implementation

#### STEP 1

Open your `.bashrc` file using your favorite editor. In this case, I'm using vim.

```bash
vi ~/.bashrc
```

#### STEP 2

At the end of your `.bashrc` place the following snippets.

```bash
export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which javac))))
```

Then save.

#### STEP 3

Source your `.bashr` and check if your `JAVA_HOME`'s set.

```bash
source ~/.bashrc
printenv JAVA_HOME
```

Your `JAVA_HOME` should conatin the directory of you JDK installation.

### System-wide Implementation 

Almost same with our previous steps, but instead of editing our `.bashrc` we'll be creating a script file on `/etc/profile.d`

#### STEP 1

Create a script file on `/etc/profile.d` and open the file, or you can do both in one go. But for the sake of this tutorial will do the long one.

```bash
touch java.sh
vi java.sh
```

_Note: If you're not root, you have to `sudo` on the commands._

#### STEP 2

Place this on the file

```bash
#!/usr/local/env bash

export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which javac))))
```

Then save.

#### STEP 3

Source the `java.sh` and check if `JAVA_HOME`'s set. You can also logout then log back-in again to check if the script's loaded.

```bash
source java.sh
printenv  JAVA_HOME
```

Once done, make sure the output shows the location of your Java or JDK installation.
