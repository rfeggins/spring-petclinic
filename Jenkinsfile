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
     stage('JIRA') {
        steps {
          def jiraID = 'DDTL-4386'
          def jiraUser = 'Jenkins'
          def newURL = "http://www.mycompany.com/support?id=1"

          //try {
          // add remote link
            def remoteLink =  [globalId: "system=http://www.mycompany.com/support&id=1",
                       application: [type: "com.acme.tracker",
                                     name: "My Acme Tracker"],
                       relationship: "causes",
                       object: [url: newURL,
                                title: "MYTEST-111"]]

           def issueLink = jiraNewRemoteIssueLink idOrKey: 'TEST-27', remoteLink: remoteLink
           echo issueLink.data.toString()
        //  } catch(Exception e) {
            // Add watcher
            jiraAddWatcher idOrKey: jiraID, userName: jiraUser
        //  }
        }
     }
     stage ('Deploy') {
       steps {
         echo "deploy"
       }
     }
  }
}
