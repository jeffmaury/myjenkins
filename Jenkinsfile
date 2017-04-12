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
        dir(path: 'build-ci') {
          git 'https://github.com/jbosstools/jbosstools-build-ci.git'
        }
        
      }
    }
    stage('sub-repos') {
      steps {
        dir(path: 'jbosstools-openshift') {
          git 'https://github.com/jbosstools/jbosstools-openshift.git'
          sh '''#!/bin/bash
../build-ci/util/findlostpatchesonerepository.sh jbosstools-4.4.x master
../build-ci/util/findlostpatchesonerepository.sh master jbosstools-4.4.x
'''
        }
        
      }
    }
  }
}