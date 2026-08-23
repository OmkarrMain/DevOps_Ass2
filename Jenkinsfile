pipeline {
    agent any

    stages {

        stage('Check Docker') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Check WSL') {
            steps {
                bat 'wsl ansible --version'
            }
        }

        stage('Check WSL Docker') {
            steps {
                bat 'wsl docker --version'
            }
        }
    }

    post {
        success {
            echo 'Jenkins can access Docker and WSL successfully!'
        }

        failure {
            echo 'Jenkins environment check failed!'
        }
    }
}
