pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('error') {
      steps {
        sh 'cd curriculum-front && npm i && npm run test:unit'
      }
    }

  }
}