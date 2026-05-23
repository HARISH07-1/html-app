pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t demo-html .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker rm -f html-container

                docker run -d --name html-container -p 9876:80 demo-html
                '''
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
