pipeline {
    agent any

    environment {
        EC2_USER = "ubuntu"
        EC2_HOST = "3.145.95.2"
    }

    stages {
        stage('Deploy to EC2') {
            steps {
                script {
                    sshagent (credentials: ['ec2-ssh-private-key']) {
                        sh """
                        ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} '
                            /home/ubuntu/deploy.sh
                        '
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Django deployed successfully on EC2!"
        }
        failure {
            echo "❌ Deployment failed."
        }
    }
}
