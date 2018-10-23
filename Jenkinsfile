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
         junit '**/target/surefire-reports/TEST-*.xml'
       }
     }
  }
}
