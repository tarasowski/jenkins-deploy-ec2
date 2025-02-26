pipeline {
    agent any

    environment {
        EC2_USER = 'ubuntu'
        EC2_HOST = '54.234.21.215' // change the ip of the machine
        DEPLOY_PATH = '/home/ubuntu/app' // change the path if needed
        SSH_CREDENTIALS = 'jenkins-ec2-key'  // Use the same ID from step 5
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/tarasowski/jenkins-nodejs.git' // add some other git repository for deployment
            }
        }

        stage('Deploy to EC2') {
            steps {
                script {
                    sshagent(credentials: [SSH_CREDENTIALS]) {
                        sh """
                        ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} 'mkdir -p ${DEPLOY_PATH}'
                        scp -o StrictHostKeyChecking=no -r * ${EC2_USER}@${EC2_HOST}:${DEPLOY_PATH}
                        """
                    }
                }
            }
        }
    }
}
