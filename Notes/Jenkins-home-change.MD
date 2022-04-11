# Changing jenkins home dir on ubuntu

Step 1 : Stop jenkins Service

```bash
    Sudo systemctl stop jenkins
```

Step 2: Create a directory for the new Jenkins home  eg :(/home/jenkins_home)

```bash
    Mkdir /home/jenkins_home
```

Step 3: change the ownership of the directory

```bash
    Chown jenkins:jenkins /home/jenkins_home
```

Step 4: change the jenkins user home directory to the new home

```bash
    Usermod -d /home/jenkins_home jenkins
```

Step 5: Copy all the files and folders from jenkins default home(/var/lib/jenkins) to the new home(/home/jenkins_home) dir.

```bash
    Sudo cp -prv /var/lib/jenkins/* /home/jenkins_home
```

Step 6: change the home location in the defaults for Jenkins automation server.

```bash
    Sudo vim /etc/default/jenkins
```

And change the following

```bash
    # jenkins home location
    #JENKINS_HOME=/var/lib/$NAME
    JENKINS_HOME=/home/jenkins_home
```

Save and exit

Step 7:  Viewing systemd services to check the jenkins home env variable.

Note: Beginning with Jenkins 2.332.1 and Jenkins 2.335, the Linux package installers use systemd to manage services.

```bash
    systemctl cat jenkins
```

Step 8 : Changing the system service.

```bash
    Systemctl edit jenkins
```

Note: The override.conf file is stored at /etc/systemd/system/jenkins.service.d/override.conf and can be used to customize the service.

Note: customizations must be done in a [Service] section in order to take effect.

```bash
    [Service]
    # Directory where Jenkins stores its configuration and workspaces
    Environment="JENKINS_HOME=/home/jenkins_home"
    WorkingDirectory=/home/jenkins_home
```

Step 9: Starting the Service.

```bash
    Sudo systemctl start jenkins
```

Step 10 : Verify the changes

```bash
    Jenkins —> manage Jenkins —> System Properties.
```
