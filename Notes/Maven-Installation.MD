# Maven installation on Jenkins Master

Apache Maven tool used primarily for Java projects, so java must be install on the system.

Installing java and check version.

```bash
sudo apt install default-jdk -y
java -version
```

## Installing Apache Maven on Ubuntu 20.04 with apt

Installing Maven on Ubuntu using apt is a simple, straightforward process.

```bash
sudo apt update -y 
sudo apt install maven -y
```

Verify Maven version.

```bash
mvn -version
```

## Installing the Latest Release of Apache Maven source code

Before continuing with the next step, visit the [Maven download](https://maven.apache.org/download.cgi) page to see if a newer version is available.

Create a dir on the system to download the source code.

```bash
sudo su -
mkdir /opt/maven
```

Download the latest Maven source code by copying the link address of the package from the download page.

```bash
cd /opt/maven
wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz
```

Extract the archive.

```bash
tar -xvzf apache-maven-3.8.5-bin.tar.gz
```

## Setup env variables

Create a maven .sh file in the /etc/profile.d directory so that maven env variables are exported every time the system starts.

```bash
sudo vim /etc/profile.d/maven.sh
```

Add the following lines.

```bash
export M2_HOME=/opt/Maven/apache-maven-3.8.5
export MAVEN_HOME=/opt/Maven/apache-maven-3.8.5
export PATH=${M2_HOME}/bin:${PATH}
```

Make the script executable.

```bash
sudo chmod +x /etc/profile.d/maven.sh
```

Load the environment variables.

```bash
source /etc/profile.d/maven.sh
```

Finally, Verify the installation.
