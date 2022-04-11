# Installing Jenkins on ubuntu 18.04

Step 1: Install java
version 11 (recommended)
    sudo sudo apt install default-jdk

  Or
version 8
    sudo apt install openjdk-8-jdk

Step 2: Verify the installation
    java -version

Step 3: Add the repository key to the system

    Sudo wget -qO - https://pkg.jenkins.io/debian-stable/jenkins.io.key | apt-key add -

Step 4: Add the Debian repository address to the server’s sources.list

    Sudo echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list

Step 5: Update and install Jenkins
    sudo apt-get update
    sudo apt-get install jenkins

Step 6: start Jenkins
    sudo systemctl start jenkins

Step 7: enable Jenkins to start automatically
    Sudo systemctl enable Jenkins

Step 8: Check Jenkins service status.
    Sudo systemctl status Jenkins

Step 9 :Get Jenkins Administrative password
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Step 10: continue jenkins setup in a browser
    <http://JenkinsServerIP:8080>
