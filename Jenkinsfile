pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t omkarr7/devops-app:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push omkarr7/devops-app:latest'
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh '''
                    ansible-playbook \
                    -i inventory.ini \
                    deploy.yml
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}
