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
  environment {
    NEXUS_VERSION = 'nexus3'
    NEXUS_PROTOCOL = 'http'
    NEXUS_URL = '172.31.40.209:8081'
    NEXUS_REPOSITORY = 'vprofile-release'
    NEXUS_REPO_ID = 'vprofile-release'
    NEXUS_CREDENTIAL_ID = 'nexuslogin'
    ARTVERSION = "${env.BUILD_ID}"
  }
}