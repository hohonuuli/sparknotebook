
# sparknotebook

This project contains samples of ipython notebooks running [Spark](https://spark.apache.org/). One notebook, _2-Text-Analytics.ipynb_ is written in python. The second, _Scala-2-Text-Analytics.ipynb_ is in Scala. The dataset and the most excellent _2-Text-Analytics.ipynb_ are originally from [https://github.com/xsankar/cloaked-ironman](https://github.com/xsankar/cloaked-ironman).

Just open each notebook to see how Spark is instantiated and used.

![Notebook](https://pbs.twimg.com/media/B1O87jsCQAAeLfz.png:large)

## Python Set-up

To run the python notebook, you will need to:

1. Install ipython and ipython notebook. For simplicity, I am just using the free [Anaconda python distribution from Continuum Analytics](http://continuum.io/downloads).
2. [Download and install Spark distribution](https://spark.apache.org/downloads.html). The download includes the `pyspark` script that you need to launch python with Spark.

For best results, cd into this projects root directory before starting ipython. The actual command to start the ipython notebook is:

```bash
IPYTHON=1 IPYTHON_OPTS="notebook --pylab inline" pyspark
```

__NOTE__: Sometimes when running Spark on Java 7 you may get a java.net.UnknownHostException. I have not yet seen this on Java 8. If this happens to you, you can resolve it by setting the __SPARK_LOCAL_IP__ environment variable to `127.0.0.1` before launching Spark. For example:

```bash
SPARK_LOCAL_IP=127.0.0.1 IPYTHON=1 IPYTHON_OPTS="notebook --pylab inline" pyspark
```

## Scala Set-up

To run the scala notebook, you will need to:

1. Create a Scala profile for ipython
```bash
ipython profile create scala
```
The output from this command will tell you the location of the _ipython_config.py_ file. You will need to edit that file soon.  
2. Download [IScala.jar](https://github.com/mattpap/IScala/releases). You will need to stash it somewhere. I put it in `~/.ipython/profile_scala/lib`  
3. Edit your _ipython_config.py_ to tell ipython about IScala
```python
c = get_config()

c.KernelManager.kernel_cmd = ["java", "-jar",
                              "/User/yournamehere/.ipython/profile_scala/lib/IScala.jar",
                              "--profile",
                              "{connection_file}",
                              "--parent"]
```

At this point you can start up IScala
```bash
ipython notebook --profile scala
```

If you are running your notebook and it crashes with OutOfMemoryErrors you can increase the amount of memory used with the `-Xms` flag (e.g. -Xmx2g or -Xmx2048m will both allocate 2GB of memory for the JVM to use):
```bash
SBT_OPTS=-Xmx2048m ipython notebook --profile scala
```

