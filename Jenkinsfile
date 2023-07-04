pipeline{
  agent any
  stages{
    stage('push to hub'){
      steps{
                withDockerRegistry(credentialsId: 'DHToken', url: 'https://index.docker.io/v1/') {
                   sh 'docker build -t angular-app-aks ./frontend/'
                  sh 'docker build -t spring-app-aks ./backend/'
            sh 'docker tag angular-app wetmonkey/spring-app-aks'
           sh 'docker tag angular-app wetmonkey/angular-app-aks'
          sh 'docker push wetmonkey/spring-app-aks:latest'
          sh 'docker push wetmonkey/angular-app-aks:latest'
                }
      }
    }
    stage('Deployment AKS'){
      steps{
      
         withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'K8S-Kubernet', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
         sh ('kubectl apply -f deployment.yaml')}
      }
    }
  }
}
