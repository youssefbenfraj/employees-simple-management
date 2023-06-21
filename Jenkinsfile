pipeline{
  agent any
  stages{
    stage('build spring'){
      steps{
        sh 'docker build -t spring-app-wm ./backend/'
      }
    } 
    stage('build angular'){
        steps{
          sh 'docker build -t angular-app-wm ./frontend/'
        }
      }
    stage('push images'){
      steps{
        withDockerRegistry(credentialsId: 'DockerHub', url: 'https://index.docker.io/v1/') {
          sh 'docker push spring-app-wm'
          sh 'docker push angular-app-wm'
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
