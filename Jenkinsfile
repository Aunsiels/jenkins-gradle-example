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
        sh 'bash gradlew :build'
      }
    }
    stage('Test') {
      steps {
        sh 'bash gradlew :test'
        junit 'build/test-results/test/*xml'
      }
    }
  }
  environment {
    GRADLE_USER_HOME = '/jenkins/.gradle'
  }
}