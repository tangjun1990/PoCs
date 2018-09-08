pipeline {
  agent any
  stages {
    stage('Deploy') {
      steps {
        sshagent (credentials: ['59e2d691-cf50-41c3-86cc-76ed393c278a']) {
          script { 
            if (env.BRANCH_NAME == "master") {
              sh 'ssh ecsop@e17 "if [ ! -d /data/site/'+JOB_NAME+' ]; then mkdir -p /data/site/'+JOB_NAME+'; fi"'
              sh 'rsync -alz --delete --exclude-from=.exclude . ecsop@e17:/data/site/'+JOB_NAME
              sh 'ssh ecsop@e17 "sudo chmod -R 777 /data/site/store/develop/storage/"'
              sh 'ssh ecsop@e17 "sudo chmod -R 777 /data/site/store/develop/bootstrap/cache/"'
            }
          }
        }
      }
    }
  }
}

