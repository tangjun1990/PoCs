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
            sh 'ssh jenkins@c162 "if [ ! -d /data/site/'+JOB_NAME+' ]; then mkdir -p /data/site/'+JOB_NAME+'; fi"'
            sh 'rsync -alz --delete --exclude-from=.exclude . jenkins@c162:/data/site/'+JOB_NAME
            sh 'ssh jenkins@c162 "sudo chmod -R 777 /data/site/store/develop/storage/"'
          }
          if (env.BRANCH_NAME == "master") {
            sh 'ssh tangjun1@c168 "if [ ! -d /opt/project/'+JOB_NAME+' ]; then mkdir -p /opt/project/'+JOB_NAME+'; fi"'
            sh 'rsync -alz --delete --exclude-from=.exclude . tangjun1@c168:/opt/project/'+JOB_NAME
            sh 'ssh tangjun1@c168 "sudo chmod -R 777 /opt/project/po/master"'
          }
        }
      }
    }
  }
}
