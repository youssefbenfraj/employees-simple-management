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
        withDockerRegistry(credentialsId: 'f03b9f2f-ea10-4037-ae74-86ce29659d74', url: 'https://index.docker.io/v1/') {
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
