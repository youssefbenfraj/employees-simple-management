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
     stage('deploy spring'){
      steps {
        sh 'docker run -d -p 8080:8080 --name SpringEmpl spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d -p 4200:80 --name AngularEmpl angular-app'
      }
    }
  }
}
