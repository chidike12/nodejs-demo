pipeline {
    agent {label "Node"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-dyke30')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/chidike12/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t dyke30/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push dyke30/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

