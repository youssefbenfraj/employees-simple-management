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
              sh 'docker network create EmployeeNetwork3 || true'
      }
    }
     stage('deploy spring'){
      steps {
        sh 'docker run -d --network EmployeeNetwork3 -p 8080:8080 --name SpringEmployee3 spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d --network EmployeeNetwork3 -p 4200:80 --name AngularEmployee3 angular-app'
      }
    }
  }
}
