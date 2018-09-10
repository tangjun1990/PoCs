pipeline {
  agent any
  stages {
    stage('Check Syntax') {
      steps {
        script {
          sh 'echo "phplang"'
        }
      }
    }
    stage('Check Code Style') {
      steps {
        script {
          sh 'echo "phpcs"'
          sh 'echo "phpmd"'
        }
      }
    }
    stage('Unit Test') {
      steps {
        script {
          sh 'echo "phpunit"'
        }
      }
    }
    stage('Build') {
      steps {
        script {
          sh 'echo "composerinstall"'
          sh 'echo " mkdirlogdir"'
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          if (env.BRANCH_NAME == "develop") {
            sh 'ssh tangjun1@bj-m-212918a "if [ ! -d /opt/project/'+JOB_NAME+' ]; then mkdir -p /opt/project/'+JOB_NAME+'; fi"'
            sh 'rsync -alz --delete --exclude-from=.exclude . tangjun1@bj-m-212918a:/opt/project/'+JOB_NAME
            sh 'ssh tangjun1@bj-m-212918a "sudo chmod -R 777 /opt/project/po/master"'
          }
          if (env.BRANCH_NAME == "master") {
            sh 'ssh tangjun1@bj-m-212918a "if [ ! -d /opt/project/'+JOB_NAME+' ]; then mkdir -p /opt/project/'+JOB_NAME+'; fi"'
            sh 'rsync -alz --delete --exclude-from=.exclude . tangjun1@bj-m-212918a:/opt/project/'+JOB_NAME
            sh 'ssh tangjun1@bj-m-212918a "sudo chmod -R 777 /opt/project/po/master"'
          }
        }
      }
    }
  }
}
