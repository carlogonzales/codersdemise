# More Verbose Error Message On Hive

Most of the time it's hard to find what goes wrong with your Hive script. Hive's using Log4J as it's logging library and defaults to `INFO` and `DRFA` as its appender. The default log file can be found at `/tmp/<user name>/hive.log`. To get a more verbose ouput on errors you have to change Hive's configuration `hive.root.logger` to `ERROR` and `CONSOLE` as appender. You can do this in three ways:

#### Hive CLI or Beeline

```bash
set hive.root.logger=WARN,console
```

#### Command Parameter

```bash
hive --hiveconf hive.root.logger=WARN,console
```

#### Hive Configuration File

Locate your hive configuration folder, and add the following config on your `hive-site.xml`.

```xml
<property>
  <name>hive.root.logger</name>
  <value>WARN,console</value>
</property>
```

