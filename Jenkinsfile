pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t demo-html .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker stop html-container || exit 0
                docker rm html-container || exit 0

                docker run -d --name html-container -p 9876:80 demo-html
                '''
            }
        }
    }
}
