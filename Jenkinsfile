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
    stage('create network'){
      steps{
              sh 'docker network create EmployeeNetwork2 || true'
      }
    }
     stage('deploy spring'){
      steps {
        sh 'docker run -d --network EmployeeNetwork2 --name SpringEmployee2 spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d --network EmployeeNetwork2 -p 4200:80 --name AngularEmployee2 angular-app'
      }
    }
  }
}
