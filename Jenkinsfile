pipeline {
    agent any

    environment {
        docker = credentials('docker')
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
            sh 'docker login -u $docker_USER --password-stdin $docker_PASSWORD'
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
