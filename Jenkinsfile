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

        // stage('Login'){
        // steps {
        //     sh '$docker_PSW | docker login -u $docker_USR --password-stdin'
        //     }
        // }
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
