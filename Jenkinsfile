pipeline {
  agent {
    docker {
      args '-v /jenkins/.gradle:/jenkins/.gradle'
      image 'gradle:latest'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh './gradlew :build'
      }
    }
    stage('Test') {
      steps {
        sh './gradlew :test'
        junit 'build/test-results/test/*xml'
      }
    }
    stage('Static Tests') {
      steps {
        sh './gradlew :check'
        recordIssues enabledForFailure: true, tool: checkStyle(pattern: 'build/reports/checkstyle/main.xml'), sourceCodeEncoding: 'UTF-8'
      }
    }
  }
  environment {
    GRADLE_USER_HOME = '/jenkins/.gradle'
  }
}
