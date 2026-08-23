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
                bat 'docker build -t omkarr7/devops-app:latest .'
            }
        }

        stage('Login and Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat '''
                        docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                        docker push omkarr7/devops-app:latest
                    '''
                }
            }
        }

        stage('Deploy using Ansible') {
            steps {
                bat '''
                    wsl ansible-playbook ^
                    -i /mnt/c/Mithibai/Practicales/SEM_3/DevOps/Assignment_2/inventory.ini ^
                    /mnt/c/Mithibai/Practicales/SEM_3/DevOps/Assignment_2/deploy.yml
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