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
        dir(path: 'util') {
          git 'https://github.com/jbosstools/jbosstools-openshift.git'
          dir(path: 'jbosstools-openshift') {
            sh '''../../findlostpaches.sh jbosstools-4.4.x master
../../findlostpaches.sh master jbosstools-4.4.x'''
          }
          
        }
        
      }
    }
  }
}