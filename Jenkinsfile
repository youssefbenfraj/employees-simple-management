pipeline{
  agent any
  stages{
    stage('build spring'){
      steps{
        sh 'docker build -t spring-app ./backend/'
      }
    } 
    stage('build angular'){
        steps{
          sh 'docker build -t angular-app ./frontend/'
        }
      }
    stage('push images'){
      steps{
         withCredentials([usernamePassword(credentialsId: 'ACR', usernameVariable: 'ACR_USERNAME', passwordVariable: 'ACR_PASSWORD')]) {
          // Authenticate with ACR using the credentials
          sh 'docker login jenkinsemployeeacr.azurecr.io --username $ACR_USERNAME --password $ACR_PASSWORD'

          sh 'docker push spring-app'
          sh 'docker push angular-app'
        }
      }
    }
    stage('Deployment AKS'){
      steps{
          withCredentials([kubeconfigFile(credentialsId: 'K8S', variable: 'KUBECONFIG')]) {
          sh 'kubectl --kubeconfig=$KUBECONFIG apply -f path/to/deployment.yaml'}
      }
    }
  }
}
