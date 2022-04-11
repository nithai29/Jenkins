# Installing Jenkins on ubuntu 18.04

Step 1: Install java

version 11 (recommended)

```bash
    sudo sudo apt install default-jdk
```

  Or

version 8

```bash
    sudo apt install openjdk-8-jdk
```

Step 2: Verify the installation

```bash
    java -version
```

Step 3: Add the repository key to the system

```bash
    Sudo wget -qO - https://pkg.jenkins.io/debian-stable/jenkins.io.key | apt-key add -
```

Step 4: Add the Debian repository address to the server’s sources.list

```bash
    Sudo echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
```

Step 5: Update and install Jenkins

```bash
    sudo apt-get update
    sudo apt-get install jenkins
```

Step 6: start Jenkins

```bash
    sudo systemctl start jenkins
```

Step 7: enable Jenkins to start automatically

```bash
    Sudo systemctl enable Jenkins
```

Step 8: Check Jenkins service status.

```bash
    Sudo systemctl status Jenkins
```

Step 9 :Get Jenkins Administrative password

```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Step 10: continue jenkins setup in a browser

```bash
    http://<Jenkins_Server_IP>:8080
```
