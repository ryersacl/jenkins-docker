pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('ryersacl')
    }
    stages { 
       stage('Build podman image') {
            steps {  
                sh 'sudo podman build -t ryersacl/flask:$BUILD_NUMBER .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo podman login docker.io -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                //sh 'sudo podman tag localhost/ryersacl/flask:$BUILD_NUMBER docker.io/ryersacl/flask:$BUILD_NUMBER'
                sh 'sudo podman push ryersacl/flask:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'sudo podman logout docker.io'
        }
    }
}
