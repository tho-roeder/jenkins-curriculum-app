pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('') {
      steps {
        bat 'bat \'\'\'@echo off dir /a\'\'\''
      }
    }

  }
}