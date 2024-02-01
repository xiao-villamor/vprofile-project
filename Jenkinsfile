pipeline {
  agent any
  stages {
    stage('BUILD') {
      post {
        success {
          echo 'Now Archiving...'
          archiveArtifacts '**/target/*.war'
        }

      }
      steps {
        sh 'mvn clean install -DskipTests'
      }
    }

    stage('UNIT TEST') {
      steps {
        sh 'mvn test'
      }
    }

    stage('INTEGRATION TEST') {
      steps {
        sh 'mvn verify -DskipUnitTests'
      }
    }

    stage('CODE ANALYSIS WITH CHECKSTYLE') {
      post {
        success {
          echo 'Generated Analysis Result'
        }

      }
      steps {
        sh 'mvn checkstyle:checkstyle'
      }
    }

  }
}