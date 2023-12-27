pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            bat 'dir /a'
          }
        }

        stage('') {
          steps {
            bat ' cd /d C:\\\\path\\\\to\\\\curriculum-front                     npm install                     npm run test:unit'
          }
        }

      }
    }

  }
}