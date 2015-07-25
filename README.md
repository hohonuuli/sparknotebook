
# sparknotebook

## IMPORTANT

I am in the process of removing the [IScala](https://github.com/mattpap/IScala) as it's development appears stalled. I'm replacing it with [jupyter-scala](https://github.com/alexarchambault/jupyter-scala). __However, jupyter-scala doesn't build for Scala 2.10 yet. Spark requires Scala 2.10.__

This project contains samples of jupyter notebooks running [Spark](https://spark.apache.org/). One notebook, _2-Text-Analytics.ipynb_ is written in python. The second, _Scala-2-Text-Analytics.ipynb_ is in Scala. The dataset and the most excellent _2-Text-Analytics.ipynb_ are originally from [https://github.com/xsankar/cloaked-ironman](https://github.com/xsankar/cloaked-ironman).

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

1. Install [jupyter-scala](https://github.com/alexarchambault/jupyter-scala)
```
git clone https://github.com/alexarchambault/jupyter-scala.git
cd jupyter-scala
sbt cli/packArchive
sbt publishM2
# unpack cli/target/jupyter-scala_2.11.6-0.2.0-SNAPSHOT.zip
cd cli/target/jupyter-scala_2.11.6-0.2.0-SNAPSHOT/bin
./jupyter-scala
```
2. Start jupyter (formerly ipython)
```
ipython notebook
# When the notebook starts you may need to select the "Scala 2.11" kernel
```

If you are running your notebook and it crashes with OutOfMemoryErrors you can increase the amount of memory used with the `-Xmx` flag (e.g. -Xmx2g or -Xmx2048m will both allocate 2GB of memory for the JVM to use):
```bash
SBT_OPTS=-Xmx2048m ipython notebook --profile "Scala 2.11"
```

As with the python example, if you get a java.net.UnknownHostException when starting ipython use the following command:

```bash
SPARK_LOCAL_IP=127.0.0.1 SBT_OPTS=-Xmx2048m ipython notebook --profile "Scala 2.11"
```

__NOTE:__ For the Scala notebook, you do __not__ need to download and install Spark. The Spark dependencies are managed via sbt which is running under the hood in the Spark notebook.

