jarcat
======

concatenate jar files (and other regular files) into one file to avoid JAR hell and enable lazy^H^H^H^focused development.

Example:  I want to work with a specific Hadoop+HBase cluster that is unlikely to change.  I have no idea what I want to do yet, but I'd like a Python REPL with which to do it.  P.S. Eclipse makes me cry

In the warring lands of code and config, you'll need the following:

code:
Hadoop (for the sake of simplicity, CDH4)
  Download hadoop-2.0.0-cdh4.1.2.tar.gz, explode it  
HBase (again, CDH4)
  Download hbase-0.92.1-cdh4.1.2.tar.gz, explode it

Jython (Jython 2.7a2)
  Download jython_installer-2.7a2.jar
  Package into embeddable jar:
    mkdir jython && java -jar jython_installer-2.7a2.jar -s -d jython -t standalone -e demo -e doc -e src -v
    
config:
  thankfully, Hadoop overloads the classloader to find its config
  also, note that the Jython JAR manifest specifies Main-Class: org.python.util.jython
  
thus:

jarcat my_hadoop.jar $(find hadoop-* -name "*.jar") $(find hbase-* -name "*.jar") /etc/hadoop/conf/* /etc/hbase/conf/* jython/jython.jar 


