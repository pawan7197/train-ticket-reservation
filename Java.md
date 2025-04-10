# train-ticket-reservati

 Train Ticket Reservation System - 
- Java 11 – to run the project
- Maven – to build the project
- Apache Tomcat 9 – to deploy the project
- AWS EC2 (Ubuntu) – the server I have used

1. Create EC2 server
   
- Go to AWS → EC2 → Launch Instance
- Choose Ubuntu 22.04
- Choose t2.micro (free tier)
- Create key pair ( I have given "java")

2. Connect to EC2 Server from Local Computer

ssh-key

3. Install Java and Maven on EC2

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
sudo apt install maven -y
```

Now Check versions:

java --version
mvn -v

4. Clone Project from GitHub

git clone https://github.com/your-username/Train-Ticket-Reservation-System.git
cd Train-Ticket-Reservation-System
```
5. Build the Project Using Maven

mvn clean install

Check the WAR file:

ls target/
# Output: TrainBook-1.0.0-SNAPSHOT.war

6. Download and Setup Apache Tomcat
goto tomcat and navigate to version9 then copy link adress of tarfile.

wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.104/bin/apache-tomcat-9.0.104.tar.gz
tar -xvzf apache-tomcat-9.0.104.tar.gz
mv apache-tomcat-9.0.104 tomcat9

7. Start Tomcat Server

cd tomcat9/bin
chmod +x *.sh
./startup.sh

Open in browser: http://your-ec2-ip:8080/
8. Deploy the WAR File to Tomcat

cp ~/Train-Ticket-Reservation-System/target/TrainBook-1.0.0-SNAPSHOT.war ~/tomcat9/webapps/
cd ~/tomcat9/bin
./shutdown.sh
./startup.sh

9. Now open the Project in Browser
- Visit: http://your-ec2-ip:8080/TrainBook-1.0.0-SNAPSHOT

 Allow Port 8080 (Only if site doesn’t open)
- Go to AWS console → EC2 → Security Groups
- Edit Inbound Rules
- Add new rule:
  - Type: Custom TCP
  - Port: 8080
  - Source: 0.0.0.0/0
- Click Save
Find Your EC2 Public IP
```bash
curl ifconfig.me
```
Here we can see the project live

- Project is live on AWS EC2 with Tomcat
