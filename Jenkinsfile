pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    sh 'kubectl get nodes'
                    sh 'kubectl apply -f deployment-service.yml'
                }
            }
        }

        stage('verify Deployment') {
            steps {
                sh 'kubectl get deploy'
            }
        }
    }
}
