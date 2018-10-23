pipeline {
  agent any

  parameters {
    string(name: 'myCommitMessage', defaultValue: 'Commit message: ddtl-3958 - Test integration workflow', description: '')
  }

  stages {
     stage ('Checkout') {
       steps {
         git 'https://github.com/rfeggins/spring-petclinic.git'
         echo ${myCommitMessage}
         
         //shortCommit = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
         
         // myCommitId = sh(returnStdout: true, script: 'git rev-parse HEAD')
         // sh "git rev-parse --short HEAD > .git/commit-id"
         // commit_id = readFile('.git/commit-id')
        // @echo off
        // echo GIT_COMMIT %GIT_COMMIT%
         //echo GIT_BRANCH %GIT_BRANCH%
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
