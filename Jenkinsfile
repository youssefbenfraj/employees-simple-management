pipeline{
  agent any
  stages{
    stage('push to hub'){
      steps{
                withDockerRegistry(credentialsId: 'DHToken', url: 'https://index.docker.io/v1/') {
                   sh 'docker build -t angular-app-AKS ./frontend/'
                  sh 'docker build -t spring-app-AKS ./backend/'
            sh 'docker tag angular-app wetmonkey/spring-app-AKS'
           sh 'docker tag angular-app wetmonkey/angular-app-AKS'
          sh 'docker push wetmonkey/spring-app-AKS:latest'
          sh 'docker push wetmonkey/angular-app-AKS:latest'
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
