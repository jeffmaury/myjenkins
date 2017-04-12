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
../build-ci/util/findlostpatchesonerepository.sh jbosstools-4.4.x master
../build-ci/util/findlostpatchesonerepository.sh master jbosstools-4.4.x
'''
        }
        
      }
    }
    stage('Send mail') {
      steps {
        emailext(attachLog: true, subject: 'Check diffs', to: 'jmaury@redhat.com', body: 'Log')
      }
    }
  }
}