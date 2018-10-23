pipeline {
  agent any

  parameters {
        string(name: 'myCommitId', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

  stages {
     stage ('Checkout') {
       steps {
         git 'https://github.com/rfeggins/spring-petclinic.git'
         myCommitId = sh(returnStdout: true, script: 'git rev-parse HEAD')
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
