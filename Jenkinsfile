pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t html-application .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker stop html-container || true
                docker rm html-container || true

                docker run -d \
                --name html-container \
                -p 9876:80 \
                html-application
                '''
            }
        }
    }
}
