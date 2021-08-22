# Pyspark // learning pyspark 

# How to Install and Run PySpark in Jupyter Notebook on Windows
When I write PySpark code, I use Jupyter notebook to run my code.
In this, I will show you how to install and run PySpark locally in Jupyter Notebook on Windows.

Items needed
Spark distribution from spark.apache.org

download Spark => https://archive.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz

Python and Jupyter Notebook. You can get both by installing the Python 3.x version of Anaconda distribution.
download anaconda => https://www.anaconda.com/products/individual

winutils.exe — a Hadoop binary for Windows — from Steve Loughran’s GitHub repo. Go to the corresponding Hadoop version in the Spark distribution and find winutils.exe under /bin. 
For example, https://github.com/steveloughran/winutils/blob/master/hadoop-2.7.1/bin/winutils.exe .

download winutils => https://github.com/steveloughran/winutils

The findspark Python module, which can be installed by running python -m pip install findspark either in Windows command prompt or Git bash if Python is installed.
You can find command prompt by searching cmd in the search box.

cmd

If you don’t have Java or your Java version is 7.x or less, download and install Java from Oracle. I recommend getting the latest JDK (version 1.8)

download java => https://www.oracle.com/in/java/technologies/javase/javase-jdk8-downloads.html

If you don’t know how to unpack a .tgz file on Windows, you can download and install 7-zip on Windows to unpack the .tgz file from Spark distribution in item 1 by right-clicking on the file icon and select 7-zip > Extract Here.

download 7zip => https://www.7-zip.org/

Installing PySpark
After getting all the items, let’s set up PySpark.

Unpack the .tgz file. For example, I unpacked with 7zip from step A6 and put mine under
 C:\LOCAL_SPARK

unzip tar

Move the winutils.exe downloaded to the \bin folder of Spark distribution. 
For example, C:\LOCAL_SPARK\spark-2.4.4-bin-hadoop2.7\bin\winutils.exe

Add environment variables: the environment variables let Windows find where the files are when we start the PySpark kernel. You can find the environment variable settings by putting “environ…” in the search box.

The variables to add are, in my example,

Name	Value
SPARK_HOME	C:\LOCAL_SPARK\spark-2.4.4-bin-hadoop2.7
HADOOP_HOME	C:\LOCAL_SPARK\spark-2.4.4-bin-hadoop2.7
PYSPARK_DRIVER_PYTHON	jupyter
PYSPARK_DRIVER_PYTHON_OPTS	notebook
add variable

In the same environment variable settings window, look for the Path or PATH variable, click edit and add 
%SPARK_HOME%\bin to it.

(Optional, if see Java related error in step C) Find the installed Java JDK folder from step A5, for example, C:\Program Files\Java\jdk1.8.0_121, and add the following environment variable

Name	Value
JAVA_HOME	C:\Program Files\Java\jdk1.8.0_251

Running PySpark in Jupyter Notebook
To run Jupyter notebook, open Windows command prompt or Git Bash and run jupyter notebook. If you use Anaconda Navigator to open Jupyter Notebook instead, 

Once inside Jupyter notebook, open a Python 3 notebook

open notebook

In the notebook, run the following code

import findspark
findspark.init()

import pyspark # only run after findspark.init()
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

df = spark.sql('''select 'spark' as hello ''')
df.show()
When you press run (shift+enter ), it might trigger a Windows firewall pop-up. I pressed cancel on the pop-up as blocking the connection doesn’t affect PySpark.

firewall warning

If you see the output, then you have installed PySpark on your Windows system!

***************************************************************************************************************************
