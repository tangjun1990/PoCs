pipeline {
  agent any
  stages {
    stage('Code Check') {
      steps {
        script {
          sh 'echo "phpcs"'
          sh '/Users/tangjun1/.composer/vendor/bin/phpmd /opt/weiboad/ad-api/api/src/application/plugins/ text /opt/work/phpmd-rulesets/phpmd_ruleset.xml'
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
            sh 'echo "success"'
          }
        }
      }
    }
  }
}
