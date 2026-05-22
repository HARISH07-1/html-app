pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t html-application .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker stop html-application || exit 0
                docker rm html-application || exit 0

                docker run -d --name html-container -p 9876:80 html-application
                '''
            }
        }
    }
}
