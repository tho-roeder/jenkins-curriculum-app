pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('Log') {
      steps {
        script {
          // Run 'ls -la' command
          sh 'ls -la'
        }
      }
    }
  }
}
