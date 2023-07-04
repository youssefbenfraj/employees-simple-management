pipeline{
  agent any
  stages{
    stage('push to hub'){
      steps{
                withDockerRegistry(credentialsId: 'DHToken', url: 'https://index.docker.io/v1/') {
                   sh 'docker build -t angular-app ./frontend/'
                  sh 'docker build -t spring-app ./backend/'
            sh 'docker tag angular-app wetmonkey/spring-app'
           sh 'docker tag angular-app wetmonkey/angular-app'
          sh 'docker push wetmonkey/spring-app:latest'
          sh 'docker push wetmonkey/angular-app:latest'
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
