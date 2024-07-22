pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('mehdifadli')
    }
    stages { 
        stage('Build docker image') {
            steps {  
                sh 'docker build -t mehdifadli/jenkins-docker:$BUILD_NUMBER .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push mehdifadli/jenkins-docker:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
