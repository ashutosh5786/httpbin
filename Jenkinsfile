pipeline {
    agent any

    stages {
        stage('Git Pull') {
            steps {
                git 'https://github.com/postmanlabs/httpbin'
            }
        }
        
        stage('Docker Build & Push'){
            steps {
               sh "docker build -t ashutosh5786/demo"
               sh "docker push ashutosh5786/demo ./"
            }
        }
    }
}
