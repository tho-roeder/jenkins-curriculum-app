pipeline {
  agent any
  tools {
    nodejs 'NodeJs-lts'
    dockerTool 'docker-lts'
    jdk 'jdk-lts'
  }
  /*
  environment {
    DOCKER_CERT_PATH = credentials('docker')
  }
  */
  stages {
    
    stage('Install vue-jest') {
            steps {
                script {
                    // Install vue-jest using npm
                    sh 'npm install --save-dev vue-jest'
                }
            }
    }

    stage('Check npm') {
      steps {
        sh 'npm version'
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
        git branch: 'dev', credentialsId: 'git_cred', url: 'https://github.com/tho-roeder/jenkins-curriculum-app'
        //git(url: 'https://github.com/tho-roeder/jenkins-curriculum-app/', branch: 'dev')
      }
    }

    stage('Log') {
      parallel {
        stage('Log') {
          steps {
            sh 'ls -la'
          }
        }
        /*
        stage('Tests') {
          steps {
            sh 'cd curriculum-front && npm i && npm run test:unit'
          }
        }
        */
      }
    }
    
    stage('Check Docker Daemon') {
            steps {
                script {
                    def dockerVersion = sh(script: 'docker --version', returnStatus: true)
                    
                    if (dockerVersion == 0) {
                        echo "Docker daemon is running"
                    } else {
                        error "Docker daemon is not running or accessible"
                    }
                }
            }
    }
    
    stage('Build') {
      steps {
        //sh 'docker build -f curriculum-front/Dockerfile .'
        //sh 'docker build -t thoroeder/jenkins-curriculum-app:latest .'
        
        script {
          // This step should not normally be used in your script. Consult the inline help for details.
          withDockerRegistry(credentialsId: 'docker', toolName: 'docker-lts') {
            // some block
            // sh(script:'docker build -t jenkins-curriculum-app:latest -f curriculum-front/Dockerfile .')
            // sh "docker info"
            sh(script: 'docker --version')
          }
        }
        
        /*
        script {
         'docker build -f curriculum-front/Dockerfile .'
        }
        */
      }
    }
    
  }
}
