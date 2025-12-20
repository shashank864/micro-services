pipeline {
  agent any

  stages {
    stage('Deploy To Kubernetes') {
      steps {
        withAWS(credentials: 'aws-creds', region: 'us-east-1') {
          sh '''
            aws eks update-kubeconfig --name eks-1 --region us-east-1
            kubectl apply -f deployment-service.yml -n webapps
          '''
        }
      }
    }

    stage('Verify Deployment') {
      steps {
        sh 'kubectl get svc -n webapps'
      }
    }
  }
}

