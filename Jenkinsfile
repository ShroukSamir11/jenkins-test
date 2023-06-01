pipeline {
    agent any
    environment {
        DOCKERHUB = credentials('dockerhub-cred')
    }
    stages {
        stage('get repo') {
            steps {
                git url: 'https://github.com/ShroukSamir11/jenkins-test'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t task-img .'

            }
        }
       
        stage('Push Image')
        {
            steps{
                sh 'echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push $DOCKERHUB_USR/task-img'
            }
        }
        stage ('Create deployment and service'){
            steps{
                sh 'kubectl apply -f deployment.yml'
                sh 'kubectl apply -f nodeport-svc.yml'
                sh 'docker logout'
            }
        }
    }
   
}