pipeline {
  agent any
  tools {
        nodejs 'NodeJs-lts'
        dockerTool 'docker-lts'
    }
  stages {
     stage('Check npm') {
            steps {
                sh 'npm version'
            }
        }
        stage('Check Docker Version') {
            steps {
                script {
                    // Run docker version command
                    def dockerVersion = sh(script: 'docker --version', returnStdout: true).trim()
                    echo "Docker Version: ${dockerVersion}"
                }
            }
        }
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh 'ls -la'
          }
        }

        stage('Tests') {
          steps {
            sh '''nodejs \'NodeJs-lts\' &&
cd curriculum-front && npm i && npm run test:unit'''
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile .'
      }
    }

  }
}
