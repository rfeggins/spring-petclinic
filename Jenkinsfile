pipeline {
  agent any
  parameters {
    string(name: 'MyCommitCOMMENT',
           defaultValue: 'ddtl-3958 - Test integration workflow')

  }

  stages {
     stage ('Checkout') {
       steps {
         git 'https://github.com/rfeggins/spring-petclinic.git'
         echo 'ddtl-3958 - Test integration workflow'


        // echo 'My Commit message'
        // sh echo mycommitmsg

         //shortCommit = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()

         // myCommitId = sh(returnStdout: true, script: 'git rev-parse HEAD')
         // sh "git rev-parse --short HEAD > .git/commit-id"
         // commit_id = readFile('.git/commit-id')
        // @echo off
        // echo GIT_COMMIT %GIT_COMMIT%
         //echo GIT_BRANCH %GIT_BRANCH%
      }
    }
    stage ('Jira') {
      steps {
        // Get Jira Server info
        script {
          ddtlID = 'DDTL-4386'
          jiraSite = 'HERTZ'

           def serverInfo = jiraGetServerInfo site: jiraSite, failOnError: true
        //def serverInfo = jiraGetServerInfo()
           echo "Jenkins Job Server Info"
           echo serverInfo.data.toString()

           // Get issue fields
           def watches = jiraGetIssueWatches idOrKey: ddtlID, site: jiraSite
           echo watches.data.toString()

           def issue = jiraGetIssue  idOrKey: ddtlID, site: jiraSite
           echo issue.data.toString()
         }
      }
    }
     stage ('Build') {
       steps {
         // sh 'mvn clean package'
         echo 'stubbed out mvn clean package'
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
