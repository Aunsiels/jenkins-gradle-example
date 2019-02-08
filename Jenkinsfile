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
        recordIssues enabledForFailure: true, tool: checkStyle(pattern: 'build/reports/checkstyle/*.xml'), sourceCodeEncoding: 'UTF-8'
        recordIssues enabledForFailure: true, tool: cpd(pattern: 'build/reports/cpd/*.xml'), sourceCodeEncoding: 'UTF-8'
        recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml'), sourceCodeEncoding: 'UTF-8'
        recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*xml'), sourceCodeEncoding: 'UTF-8'
      }
    }
  }
  environment {
    GRADLE_USER_HOME = '/jenkins/.gradle'
  }
}
