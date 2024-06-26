Personal Portfolio Website in NGnix
![Ngnix](https://github.com/Prasan-V/classs/assets/130823121/d0718695-0b0d-43ce-b01f-742521d9c0f7)

npm start
Runs the app in the development mode.
Open http://localhost:8085 to view it in your browser.
The page will reload when you make changes.
You may also see any lint errors in the console.

**npm test**
Builds the app for production to the build folder.
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.
Your app is ready to be deployed!

See the section about deployment for more information.

1. Launch an EC2 Instance (t2.xlarge):
   Log in to your AWS console.
   Navigate to EC2.
   Click "Launch Instance."
   Choose the "t2.xlarge" instance type.
   Configure other settings (VPC, security groups, key pair, etc.).
   Launch the instance.
 2. **Install Jenkins and Docker**:
    SSH into your EC2 instance.
Update the package list: sudo apt update.
**Install Jenkins:**
#!/bin/bash sudo apt update -y
sudo apt upgrade -y
sudo apt install openjdk-17-jre -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee
/etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y

**Install Docker**:
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" -y
sudo apt update -y
apt-cache policy docker-ce -y
sudo apt install docker-ce -y
#sudo systemctl status docker
sudo chmod 777 /var/run/docker.sock

3. **Access Jenkins**:
   Open a web browser and navigate to http://<your-ec2-public-ip>:8080.
Retrieve the initial admin password from the Jenkins server:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

4. **Install Required Plugins**:
   In Jenkins, go to "Manage Jenkins" > "Manage Plugins."
   Install necessary plugins (e.g., Pipeline, GitHub, Docker).

5. **Create a Jenkins Pipeline**:
    Create a new Jenkins job.
    Select "Pipeline" as the job type.
    Write your Groovy script in the pipeline configuration. 

6. **GitHub Integration:**
   Go to your GitHub repository.
   Under "Settings," select "Developer settings."
   Generate a classic token and copy it.
   
7. **Configure Jenkins with GitHub Credentials:**
   In Jenkins, go to "Manage Jenkins" > "Configure System."
   Add your GitHub username and paste the token as the password.
   
8. **DockerHub Integration:**
    Go to DockerHub.
   Generate an access token.

9.**Configure DockerHub in Jenkins:**
    In Jenkins, go to "Manage Jenkins" > "Configure System."
    Add your DockerHub username and paste the token.

10.**Attaching Webhook in GitHub:**

  Go to your GitHub repository.
  Under "Settings," select "Webhooks."
  Click on "Add webhook."
  Set the payload URL to your Jenkins server's URL followed by /github-webhook/.
  Select the events you want to trigger the webhook (e.g., Push events).
  Optionally, you can set up a secret and configure Jenkins to validate the webhook payload using this secret.
  Save your webhook configuration.
11. **Access Docker Container:**
    Access it via http://<your-ec2-public-ip>8085:.
    Remember to replace <your-ec2-public-ip> with your actual EC2 instance's public IP address.  





