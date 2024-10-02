pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('ryersacl')
    }
    stages { 
        stage('Clean up') {
            steps {
                sh 'sudo podman rmi docker.io/ryersacl/myapp/flask:$BUILD_NUMBER || true'
            }
        }
        stage('Build podman image') {
            steps {  
                sh 'sudo podman build -t myapp/flask:$BUILD_NUMBER .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo podman login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                sh 'sudo podman tag localhost/myapp/flask:$BUILD_NUMBER docker.io/ryersacl/myapp/flask:$BUILD_NUMBER'
                sh 'sudo podman push docker.io/ryersacl/myapp/flask:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'sudo podman logout'
        }
    }
}
