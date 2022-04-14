# Installing Tomcat on RHEL

Apache Tomcat is an open-source, lightweight, powerful and widely-used web server developed and maintained by Apache Foundation. It is an implementation of the Java Servlet, JavaServer Pages (JSP), Java Expression Language (EL) and Java WebSocket technologies, and provides a pure Java HTTP server to run Java web-based applications.

## Prerequisites

Install java

```bash
sudo yum -y update
sudo yum -y install java-1.8.0-openjdk-devel
OR
sudo yum -y install java-11-openjdk-devel
```

Verifty java.

```bash
jave -version
```

## Installing the Latest Release of Apache Tomcat source code

Before continuing with the next step, visit the [Maven download](https://tomcat.apache.org/download-90.cgi) page to see if a newer version is available.

Create a dir on the system to download the source code.

```bash
sudo su -
mkdir /opt/tomcat
```

Download the latest Tomcat source code by copying the link address of the package from the download page.

```bash
cd /opt/tomcat
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.62/bin/apache-tomcat-9.0.62.tar.gz
```

Extract the archive.

```bash
tar -xvzf apache-tomcat-9.0.62.tar.gz
```

The following is a description of each of the sub-directories in the installation directory of Apache Tomcat.

- bin – contains the executables.
- conf – contains configuration files.
- lib – stores library files.
- log – stores log files.
- temp – contains temporary files.
- webaaps – stores web application files.

Give executing permissions to startup.sh and shutdown.sh which are under bin.

```bash
chmod +x /opt/tomcat/apache-tomcat-9.0.62/bin/startup.sh 
chmod +x /opt/tomcat/apache-tomcat-9.0.62/bin/shutdown.sh
```

Create link files for tomcat startup.sh and shutdown.sh

```bash
ln -s /opt/tomcat/apache-tomcat-9.0.62/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/tomcat/apache-tomcat-9.0.62/bin/shutdown.sh /usr/local/bin/tomcatdown
```

Start tomcat

```bash
tomcatup
```

verify

```bash
http://<Public_IP>:8080
```

Note. Tomcat and Jenkins runs on ports number 8080 and Using unique ports for each application is a best practice in an environment. Hence lets change tomcat port number to 8090. Change port number in conf/server.xml file under tomcat home.

```bash
cd /opt/tomcat/apache-tomcat-9.0.62/conf
# update port number in the "connecter port" field in server.xml
# restart tomcat after configuration update
```

Reloading Tomcat service.

```bash
tomcatdown
tomcatup
```

verify

```bash
http://<Public_IP>:8090
```

After verifying the application is accessible on port 8090. Login to Tomcat, but tomcat application doesnt allow login from remote browser and only allows local browser login, to address this issue change a default parameter in context.xml.

```bash
# search for context.xml
find / -name context.xml
OR
locate context.xml #need mlocate installed prior
```

Locate and comment () Value ClassName field which are under webapp directory in the following files.

```bash
/opt/tomcat/apache-tomcat-9.0.62/webapps/host-manager/META-INF/context.xml
/opt/tomcat/apache-tomcat-9.0.62/webapps/manager/META-INF/context.xml
```

eg:

```bash
<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
     allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />-->
```

Reloading Tomcat service.

```bash
tomcatdown
tomcatup
```

Add users information to conf/tomcat-users.xml.

```bash
<role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-script"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>
```

Reloading Tomcat service.

```bash
tomcatdown
tomcatup
```
