pipeline {
    agent any

    environment {
        KUBECONFIG = '/home/adminharish/.kube/config'
    }

    stages {

        stage('Check Kubernetes Cluster') {
            steps {
                bat '''
                kubectl get nodes
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t demo-html .
                '''
            }
        }

        stage('Load Image into Minikube') {
            steps {
                bat '''
                minikube image load demo-html
                '''
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                bat '''
                kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                '''
            }
        }

        stage('Check Kubernetes Resources') {
            steps {
                bat '''
                kubectl get pods
                kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo 'Kubernetes deployment successful!'
        }

        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
