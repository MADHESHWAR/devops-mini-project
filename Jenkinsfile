pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Already checked out'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker rm -f devops-container || true
                docker run -d -p 8083:80 --name devops-container devops-app
                '''
            }
        }

        stage('Terraform Init') {
            steps {
                dir('terraform') {
                    bat 'terraform init'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                dir('terraform') {
                    bat 'terraform apply -auto-approve'
                }
            }
        }
    }
}
