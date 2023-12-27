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

        stage('Tests') {
          steps {
            bat '''
              cd /d C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\jenkins-curriculum-app_dev\\curriculum-front
              npm install
              npm run test:unit
            '''
          }
        }

      }
    }

    stage('') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile .'
      }
    }

  }
}