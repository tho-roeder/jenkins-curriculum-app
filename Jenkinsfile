pipeline {
  agent any
    tools {
    nodejs 'NodeJs-lts'
    dockerTool 'docker-lts'
    jdk 'jdk-lts'
  }
  
  stages {
    stage('Check npm') {
      steps {
        sh 'npm version'
      }
    }
    stage('Install vue-jest') {
            steps {
                script {
                    // Install vue-jest using npm
                    sh 'npm install --save-dev vue-jest'
                }
            }
        }
    
    stage('Run Tests') {
        steps {
            script {
                // Run your tests using vue-cli-service or other test runner
                sh 'npm run test:unit'
            }
        }
    }
      
    stage('Check Docker Version') {
      steps {
        script {
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
            sh 'cd curriculum-front && npm i && npm run test:unit'
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
