pipeline {
  agent any
  tools {
    nodejs 'NodeJs-lts'
    dockerTool 'docker-lts'
    jdk 'jdk-lts'
    // a bit ugly because there is no `@Symbol` annotation for the DockerTool
    // see the discussion about this in PR 77 and PR 52: 
    // https://github.com/jenkinsci/docker-commons-plugin/pull/77#discussion_r280910822
    // https://github.com/jenkinsci/docker-commons-plugin/pull/52
    'org.jenkinsci.plugins.docker.commons.tools.DockerTool' '18.09
  }
  
  environment {
    DOCKER_CERT_PATH = credentials('docker')
  }
  
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
    /*
    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile .'
      }
    }
    */
  }
}
