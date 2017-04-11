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
    stage('sub-repos') {
      steps {
        ws(dir: 'repos') {
          ws(dir: 'openshift') {
            git 'https://github.com/jbosstools/jbosstools-openshift.git'
            echo 'pwd()'
          }
          
        }
        
      }
    }
  }
}