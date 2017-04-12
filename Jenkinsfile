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
          git(url: 'https://github.com/jeffmaury/jbosstools-build-ci.git', branch: 'findlostpatches-dryrun')
        }
        
      }
    }
    stage('sub-repos') {
      steps {
        dir(path: 'jbosstools-openshift') {
          git 'https://github.com/jbosstools/jbosstools-openshift.git'
          sh '''#!/bin/bash
ls -l /bin/*
'''
        }
        
      }
    }
  }
}