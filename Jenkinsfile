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
          sh '''set +x
set +e
ls -l /bin/*
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
sh ../build-ci/util/findlostpatchesonerepository.sh jbosstools-4.4.x master
sh ../build-ci/util/findlostpatchesonerepository.sh master jbosstools-4.4.x'''
        }
        
      }
    }
  }
}