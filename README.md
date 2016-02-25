# Debugging Spark with IntelliJ

PreRequisite: 
You have assembled your code with all the dependencies into the same jar.

If you want to debug a driver program: 
You must use this option into your spark.submit and you have to configurate your IDE to remote debugging pointing to the port (in this case 5005) and the IP address of your server:

--driver-java-options -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=5005

In this case, you need to launch your spark-submit with --master local[<DesiredNumberOfCores>] 

But if you need to debug your .jar in a executor: 
In this case you have to configurate your IDE remote debugging in listening mode:
Remember to use --num-excutors 1 to receive only 1 executor data

--num-executors 1 --executor-cores 1 --conf "spark.executor.extraJavaOptions=-agentlib:jdwp=transport=dt_socket,server=n,address=<YourLocalComputerAddress>:5005,suspend=n"

Although it's deprecated for the moment (Spark 1.6.0) you can use:
export SPARK_JAVA_OPTS=-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005
