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
    stage('Deployment'){
      steps{
            sh 'minikube kubectl --apply -f deployment.yaml'
      }
    }
  }
}
