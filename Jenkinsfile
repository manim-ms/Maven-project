pipeline {
    agent any
    environment{
        IMAGE_NAME = "demoimage"
        DOCKERHUB_USERNAME = "kunchalavikram"
    }

   stage('Checkout') {
    steps {
        echo 'Cloning repository from GitHub...'
        git branch: 'main',
            credentialsId: 'github-token',       
            url: 'https://github.com/manim-ms/Maven-project.git'   
    }
}

        stage('build'){
            steps{
                withEnv(['PATH+EXTRA=/opt/apache-maven-3.9.5/bin']) {
                    sh 'mvn package'
                }
                sh "ls -al target/"
            }
        }
        stage('dockerize'){
            steps{
                withCredentials([string(credentialsId: 'docker_token', variable: 'TOKEN')]) {
                    sh 'docker login -u kunchalavikram -p ${TOKEN}'
                }
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
                sh 'docker tag $IMAGE_NAME:$BUILD_NUMBER $DOCKERHUB_USERNAME/$IMAGE_NAME:$BUILD_NUMBER'
            }
        }
        stage('push'){
            steps{
                sh 'docker push $DOCKERHUB_USERNAME/$IMAGE_NAME:$BUILD_NUMBER'
            }
        }
    }
}
