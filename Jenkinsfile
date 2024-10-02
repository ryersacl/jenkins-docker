pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('ryersacl')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'podman build -t myapp/flask:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | podman login docker.io -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'podman push docker.io/myapp/flask:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'podman logout'
        }
    }
}
