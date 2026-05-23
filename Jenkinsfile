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

        stage('Deploy to Kubernetes in WSL') {
            steps {
                bat '''
                wsl bash -c "cd ~/html-app && \
                minikube image load demo-html && \
                kubectl apply -f deployment.yaml && \
                kubectl apply -f service.yaml && \
                kubectl get pods && \
                kubectl get svc"
                '''
            }
        }
    }

    post {
        success {
            echo 'Kubernetes deployment successful!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
