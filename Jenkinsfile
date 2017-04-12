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
        script {
          def comps = ["Aerogear","Arquillian","Base","BrowserSim","build-sites","Central","Discovery","Forge","Freemarker","Hibernate","Integration-Tests ","JavaEE","JST","LiveReload","OpenShift","Server","versionwatch","VPE","Webservices"]
          comps.each {
            def comp = it.toLowerCase()
            dir(path: "jbosstools-${comp}") {
              git "https://github.com/jbosstools/jbosstools-${comp}.git"
              sh '''#!/bin/bash
../build-ci/util/findlostpatchesonerepository.sh jbosstools-4.4.x master
../build-ci/util/findlostpatchesonerepository.sh master jbosstools-4.4.x
'''
            }
          }
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
