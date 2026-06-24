## Steps to add email notification
- <b id="Mail">Go to your Jenkins Master EC2 instance and allow 465 port number for SMTPS</b>
# 
- <b>Now, we need to generate an application password from our gmail account to authenticate with jenkins</b>
  - <b>Open gmail and go to <mark>Manage your Google Account --> Security</mark></b>
> [!Important]
> Make sure 2 step verification must be on

  ![image](https://github.com/user-attachments/assets/5ab9dc9d-dcce-4f9d-9908-01095f1253cb)

  - <b>Search for <mark>App password</mark> and create a app password for jenkins</b>
  ![image](https://github.com/user-attachments/assets/701752da-7703-4685-8f06-fe1f65dd1b9c)
  ![image](https://github.com/user-attachments/assets/adc8d8c0-8be4-4319-9042-4115abb5c6fc)
  
#
- <b> Once, app password is create and go back to jenkins <mark>Manage Jenkins --> Credentials</mark> to add username and password for email notification</b>
![image](https://github.com/user-attachments/assets/2a42ec62-87c8-43c8-a034-7be0beb8824e)

# 
- <b> Go back to <mark>Manage Jenkins --> System</mark> and search for <mark>Extended E-mail Notification</mark></b>
![image](https://github.com/user-attachments/assets/bac81e24-bb07-4659-a251-955966feded8)
#
- <b>Scroll down and search for <mark>E-mail Notification</mark> and setup email notification</b>
> [!Important]
> Enter your gmail password which we copied recently in password field <mark>E-mail Notification --> Advance</mark>

![image](https://github.com/user-attachments/assets/14e254fc-1400-457e-b3f4-046404b66950)
![image](https://github.com/user-attachments/assets/7be70b3a-b0dc-415c-838a-b1c6fd87c182)
![image](https://github.com/user-attachments/assets/cffb6e1d-4838-483e-97e0-6851c204ab21)

# EXAMPLE PIPELINE
pipeline {
    agent any;
    stages {
        
        stage ("Clone") {
            steps {
                git branch: "master",
                url: "https://github.com//FlinalProject"
            }
        }
        
        stage ("Trivy file system scan") {
            steps {
                sh "trivy fs -o results.json ."
            }
        }
        
        stage ("build") {
            steps {
                sh "docker build -t obys-agency:latest ."
            }
        }
        
        stage ("test") {
            steps {
                echo "No test cases!!"
            }
        }
        
        stage ("deploy") {
            steps {
                sh "docker run -d --name obys-container -p 8081:80 obys-agency:latest"
            }
        }
        
    }
    
    post {
        success {
            script {
                emailext from: 'sender@gmail.com',
                to: 'reciver@gmail.com',
                body: 'Build success',
                subject: 'Build success'
            }
        }
        failure {
            script {
                emailext from: 'sender@gmail.com',
                to: 'reciver@gmail.com',
                body: 'Build failed',
                subject: 'Build failed'
            }
        }
    }
}
