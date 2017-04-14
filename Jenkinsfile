pipeline {
  agent any
  stages {
    stage('get build-ci') {
      steps {
        dir(path: 'build-ci') {
          git(url: 'https://github.com/jeffmaury/jbosstools-build-ci.git', branch: 'findlostpatches-dryrun')
        }
        
      }
    }
    stage('check components') {
      steps {
        script {
          def comps = ["Aerogear","Arquillian","Base","BrowserSim","build-sites","Central","Discovery","Forge","Freemarker","Hibernate","Integration-Tests","JavaEE","JST","LiveReload","OpenShift","Server","versionwatch","VPE","Webservices"]
          for (comp in comps) {
            comp = comp.toLowerCase()
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
  }
}
