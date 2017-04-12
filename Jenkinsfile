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
        dir(path: 'util') {
          git 'https://github.com/jbosstools/jbosstools-openshift.git'
          dir(path: 'jbosstools-openshift') {
            sh '''git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
sh ../findlostpatchesonerepository.sh jbosstools-4.4.x master
sh ../findlostpatchesonerepository.sh master jbosstools-4.4.x'''
          }
          
        }
        
      }
    }
  }
}
