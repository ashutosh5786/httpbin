pipeline {
    agent any

    environment {
        docker = credentials('pass')
    }
    stages {
        stage('Git Pull') {
            steps {
                git 'https://github.com/ashutosh5786/httpbin'
            }
        }
        
        stage('Docker Build'){
            steps {
               sh "docker build -t ashutosh5786/demo:${BUILD_NUMBER} ./"
            }
        }

        stage('Login'){
        steps {
            sh 'echo $docker | docker login -u ashutosh5786 --password-stdin'
            }
        }
        stage('Push'){
        steps {
            sh 'docker push ashutosh5786/demo:${BUILD_NUMBER}'
        }
        }

    }
    post {
        always {
            sh 'docker logout'
            sh 'docker image rm ashutosh5786/demo:${BUILD_NUMBER}'
        }
    }
}
