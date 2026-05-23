pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\Users\\HARISH\\.kube\\config'
    }

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

        stage('Load Image to Minikube') {
            steps {
                bat 'minikube image load demo-html'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml --validate=false'
            }
        }

        stage('Check Kubernetes Pods') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get svc'
            }
        }
    }
}
