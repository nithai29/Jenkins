# Installing Jenkins on ubuntu 18.04

Step 1: Install java.

version 11 (recommended)

```bash
sudo apt install default-jdk -y
```

  Or

version 8

```bash
sudo apt install openjdk-8-jdk -y
```

Step 2: Verify the installation.

```bash
java -version
```

Step 3: Add the repository key to the system by switching to root user.

```bash
sudo su -
wget -qO - https://pkg.jenkins.io/debian-stable/jenkins.io.key | apt-key add -
```

Step 4: Add the Debian repository address to the server’s sources.list.

```bash
echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
```

Step 5: Update and install Jenkins.

```bash
apt-get update -y
apt-get install jenkins -y
```

Step 6: start Jenkins and enable Jenkins to start automatically.

```bash
systemctl start jenkins && systemctl enable Jenkins
```

Step 7: Check Jenkins service status.

```bash
systemctl status Jenkins
```

Step 9 :Get Jenkins Administrative password.

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

Step 9: continue jenkins setup in a browser.

```bash
http://<Jenkins_Server_IP>:8080
```
