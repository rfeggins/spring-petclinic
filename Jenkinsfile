pipeline {
  agent any

  parameters {
    string(name: 'myCommitId', defaultValue: 'Mr Jenkins', description: '')
  }

  stages {
     stage ('Checkout') {
       steps {
         git 'https://github.com/rfeggins/spring-petclinic.git'
         // myCommitId = sh(returnStdout: true, script: 'git rev-parse HEAD')
         sh "git rev-parse --short HEAD > .git/commit-id"
         commit_id = readFile('.git/commit-id')
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
