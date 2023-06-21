pipeline{
  agent any
  stages{
    stage('build spring'){
      steps{
        sh 'docker build -t employeemonkeyspring ./backend/'
      }
    } 
    stage('build angular'){
        steps{
          sh 'docker build -t employeemonkeyangular ./frontend/'
        }
      }
    stage('push images'){
      steps{
        withDockerRegistry(credentialsId: 'DockerHub', url: 'https://index.docker.io/v1/') {
          sh 'docker push employeemonkeyspring'
          sh 'docker push employeemonkeyangular'
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
