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
              sh 'docker network create EmployNetwork || true'
      }
    }
     stage('deploy spring'){
      steps {
        sh 'docker run -d --network EmployNetwork --name SpringEmploy1 spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d --network EmployNetwork -p 4200:80 --name AngularEmploy1 angular-app'
      }
    }
  }
}
