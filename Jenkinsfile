pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Git') {
      steps {
        git(url: 'https://bitbucket.org/Ram75/bird/src', branch: 'Bird4.0', credentialsId: 'ram')
      }
    }

  }
}