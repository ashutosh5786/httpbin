pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }
    stages {
        stage('Git Pull') {
            steps {
                git 'https://github.com/postmanlabs/httpbin'
            }
        }
        
        stage('Docker Build'){
            steps {
               sh "docker build -t ashutosh5786/demo ./"
            }
        }

        stage('Login'){
        steps {
            sh '$DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push'){
        steps {
            sh 'docker push ashutosh5786/demo'
        }
        }

    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
