pipeline {
  agent any

  stages {
     stage ('Checkout') {
       steps {
         git 'https://github.com/rfeggins/spring-petclinic.git'
       }
     }
     stage ('Build') {
       steps {
         sh 'mvn clean package'
       }
     }
     stage ('Test') {
       steps {
         junit '**/target/surefire-reports/TEST-*.xml'
       }
     }
     stage ('Archive artifacts') {
       steps {
          archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
       }
     }
     stage ('Deploy') {
       steps {
         echo "deploy"
       }
     }
       }
     }
  }
}
