pipeline{
  agent any
  stages{
    stage('build images'){
      steps{
        sh 'docker build -t angular-app-ak ./frontend/'
        sh 'docker build -t spring-app-ak ./backend/'
      }
    }
    stage('push to hub'){
      steps{
          withDockerRegistry(credentialsId: 'DHToken', url: 'https://index.docker.io/v1/') {
            sh 'docker tag angular-app wetmonkey/spring-app-ak'
            sh 'docker tag angular-app wetmonkey/angular-app-ak'
            sh 'docker push wetmonkey/spring-app-ak:latest'
            sh 'docker push wetmonkey/angular-app-ak:latest'
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
