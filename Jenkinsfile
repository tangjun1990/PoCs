pipeline {
  agent any
  stages {
    stage('Check Syntax') {
      steps {
        script {
          sh 'find ./ -name "*.php" -type f -exec php -l {} \;'
        }
      }
    }
    stage('Check Code Style') {
      steps {
        script {
          sh 'phpcs ./ --standard=PSR2'
          sh 'phpmd /path/to/file text /opt/work/phpmd-rulesets/phpmd_ruleset.xml'
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
          sh 'composer install'
          sh 'cp /home/env/'+JOB_NAME+'.env xxxxxx.ini'
        }
      }
    }
    stage('Deploy') {
      steps {
        sshagent (credentials: ['59e2d691-cf50-41c3-86cc-76ed393c278a']) {
          script {
            if (env.BRANCH_NAME == "develop") {
              sh 'ssh jenkins@c162 "if [ ! -d /data/site/'+JOB_NAME+' ]; then mkdir -p /data/site/'+JOB_NAME+'; fi"'
              sh 'rsync -alz --delete --exclude-from=.exclude . jenkins@c162:/data/site/'+JOB_NAME
              sh 'ssh jenkins@c162 "sudo chmod -R 777 /data/site/store/develop/storage/"'
            }
            if (env.BRANCH_NAME == "master") {
              sh 'ssh jenkins@c168 "if [ ! -d /data/site/'+JOB_NAME+' ]; then mkdir -p /data/site/'+JOB_NAME+'; fi"'
              sh 'rsync -alz --delete --exclude-from=.exclude . jenkins@c168:/data/site/'+JOB_NAME
              sh 'ssh jenkins@c168 "sudo chmod -R 777 /data/site/store/release/storage"'
            }
          }
        }
      }
    }
  }
}
