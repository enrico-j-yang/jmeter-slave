# JMeter server/slave docker image

Server docker file should be inherited from the base image and should expose port 1099 and 50000. jmeter-server should be running..

In order to use jmeter slave docker image, following actions should be taken.

* Copy jmeter plugin jars to $JMETER_HOME/lib/ext/.
* Copy jmeter plugin dependent lib to $JMETER_HOME/lib/.
* Copy jmeter test plan to container work directory.
* Copy test data files for jmeter test plan to container work directory
