# JMeter server/slave docker image

Server docker file should be inherited from the base image and should expose port 1099 and 50000. jmeter-server should be running..

In order to use jmeter slave docker image, following actions should be taken.

* Copy jmeter plugin jars to $JMETER_HOME/lib/ext/.
* Copy jmeter plugin dependent lib to $JMETER_HOME/lib/.
* Copy jmeter test plan to container work directory.
* Copy test data files for jmeter test plan to container work directory

Run JMeter slaves


```shell
docker run -dit --rm --name slave01 jmeter_sample_slave
docker run -dit --rm --name slave02 jmeter_sample_slave
```

Run JMeter master in remote mode with -Rslaveip1,slaveip2

```shell
docker run --rm --name master jmeter_sample -n -t /app/tag.jmx -l /app/log.jtl -e -o /app/result -$(echo R$(docker inspect --format '{{ .Name }} => {{ .NetworkSettings.IPAddress }}' $(docker ps -a -q) | awk '{print $3}' | tr '\n' ',' | sed 's/,\([^,]*\)$/ \1/'))
```
