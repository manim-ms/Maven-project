pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Running Maven clean and compile...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Maven tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}

