pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
-Dsonar.host.url=http://172.31.2.90:9000/ \\
-Dsonar.projectKey=PetClinic_MavenProject1 \\
-Dsonar.login=sqp_2e46ef936200aad05b45354b78d7d7d914a22c30'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh ' ./mvnw package -DskipTests=true'
      }
    }

    stage('QA') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('Integration and Performance Tests') {
          steps {
            sh './mvnw verify'
            junit '**/target/surefire-reports/*.xml'
            perfReport '**/target/jmeter/results/*'
          }
        }

      }
    }

  }
}
