pipeline {
    agent any

    environment {
        docker = credentials('pass')
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
            sh 'echo $docker | docker login -u ashutosh5786 --password-stdin'
            }
        }
        stage('Push'){
        steps {
            sh 'docker push ashutosh5786/demo'
        }
        }

        // stage('Delete & Deploy'){
        //     steps {
        //         sh 'kubectl delete deploy demo'
        //         sh 'kubectl apply -f demo.yaml'
        //     }
        // }

    }
    post {
        always {
            sh 'docker logout'
            sh 'docker image rm ashutosh5786/demo'
        }
    }
}
