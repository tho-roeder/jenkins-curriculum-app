pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('Front-End Unit Tests') {
      steps {
        sh 'cd curriculum-front && npm i && npm run tests:unit'
      }
    }

  }
}