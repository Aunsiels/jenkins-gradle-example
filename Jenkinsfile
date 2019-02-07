pipeline {
  agent {
    docker {
      image 'gradle:lastest'
      args '-v /jenkins/.gradle:/jenkins/.gradle'
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