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
              sh 'docker network create EmployeeNetwork1 || true'
      }
    }
     stage('deploy spring'){
      steps {
        sh 'docker run -d --network EmployeeNetwork1 --name SpringEmployee1 spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d --network EmployeeNetwork1 -p 4200:80 --name AngularEmployee1 angular-app'
      }
    }
  }
}
