pipeline{
  agent any
  stages{
    stage('delete old containers'){
      steps{
        sh 'docker stop AirbusSpring || true'
        sh 'docker rm AirbusSpring || true'
        sh 'docker stop AirbusAngular || true'
        sh 'docker rm AirbusAngular || true'
        sh 'docker network rm -f EmployeeNetwork || true'
      }
    }
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
              sh 'docker network create EmployeeNetwork || true'
      }
    }
     stage('deploy spring'){
      steps {
        sh 'docker run -d --network EmployeeNetwork -p 8080:8080 --name EmployeeSpring spring-app'
      }
    }
    stage('deploy angular'){
      steps{
        sh ' docker run -d --network EmployeeNetwork -p 4200:80 --name EmployeeAngular angular-app'
      }
    }
  }
}
