pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.host.url=http://13.232.168.189:9000/ \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.login=sqp_bcf23ede991d3e28282388e7525f14fccf3fa4a5'''
      }
    }

  }
}