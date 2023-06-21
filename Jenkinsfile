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
         sh 'docker login --username $wetmonkey --password $dckr_pat_E1V-V2g2thDoYmkw8McxZnZSURg'
          sh 'docker push spring-app'
          sh 'docker push angular-app'
        
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
