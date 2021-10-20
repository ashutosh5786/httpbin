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

        stage('Deploy'){
            steps {
                sh 'ls -la'
                sh "sed -i 's/v1/${BUILD_NUMBER}/g' jenkins-deploy.yaml"
                sh 'kubectl apply -f jenkins-deploy.yaml'
                sh 'kubectl apply -f jenkins-svc.yaml'
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
