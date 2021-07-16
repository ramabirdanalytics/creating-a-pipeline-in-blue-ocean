pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'npm install'
          }
        }

        stage('Eslint') {
          steps {
            sh 'npm install --save-dev eslint-plugin-security'
          }
        }

      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          environment {
            CI = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
          }
        }

        stage('contint') {
          steps {
            sh 'npm run-script cont-int'
          }
        }

      }
    }

    stage('Deliver') {
      parallel {
        stage('Deliver') {
          steps {
            sh './jenkins/scripts/deliver.sh'
            input 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
          }
        }

        stage('VulnerabilityTest') {
          steps {
            sh 'npm test'
          }
        }

      }
    }

  }
}