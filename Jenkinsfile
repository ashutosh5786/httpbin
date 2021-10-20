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
            sh 'echo $docker_PSW > 1.txt | cat 1.txt'
            sh 'echo $docker_USER > 2.txt | cat 2.txt'
            sh 'echo $docker_USR > 3.txt | cat 3.txt'
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
