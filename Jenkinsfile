pipeline {
  agent any
  stages {
    stage('start') {
      steps {
        echo 'Started'
      }
    }
    stage('pull') {
      steps {
        git 'https://github.com/jbosstools/jbosstools-build-ci.git'
      }
    }
  }
}