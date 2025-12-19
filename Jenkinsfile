pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Deploy To Kubernetes') {
      steps {
        withKubeCredentials(kubectlCredentials: [[
          caCertificate: '',
          clusterName: 'EKS-1',
          contextName: '',
          credentialsId: 'k8-token',
          namespace: 'webapps',
          serverUrl: 'https://7469897791D88C46B523A50334896282.gr7.us-east-1.eks.amazonaws.com'
        ]]) {
          sh '''
            kubectl config current-context || true
            kubectl apply -n webapps -f .
          '''
        }
      }
    }

    stage('Verify Deployment') {
      steps {
        withKubeCredentials(kubectlCredentials: [[
          caCertificate: '',
          clusterName: 'EKS-1',
          contextName: '',
          credentialsId: 'k8-token',
          namespace: 'webapps',
          serverUrl: 'https://7469897791D88C46B523A50334896282.gr7.us-east-1.eks.amazonaws.com'
        ]]) {
          sh '''
            kubectl get ns
            kubectl get deploy -n webapps
            kubectl get pods -n webapps -o wide
            kubectl get svc -n webapps
          '''
        }
      }
    }
  }
}

}
