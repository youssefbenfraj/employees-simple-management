pipeline{
  agent any
  stages{
    stage('build spring'){
      steps{
        sh 'docker build -t spring-app ./frontend/'
      }
    } 
    stage('build angular'){
        steps{
          sh 'docker build -t angular-app ./backend/'
        }
      }
     stage('deploy spring'){
      steps {
        sh 'docker run -d -p 8080:80 --name SpringEmpl spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d -p 4200:80 --name AngularEmpl angular-app'
      }
    }
  }
}
