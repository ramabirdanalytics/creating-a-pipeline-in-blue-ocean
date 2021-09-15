pipeline {
  agent any
  stages {
    stage('Git') {
      steps {
        git(url: 'https://bitbucket.org/Ram75/bird/src', branch: 'Bird4.0', credentialsId: 'ram')
      }
    }

    stage('Invoke DC') {
      steps {
        dependencyCheck(additionalArguments: '--scan= "/var/lib/jenkins_home//workspace/Bird_Bird/datahandler/lib/*.jar" --format HTML', odcInstallation: 'Default')
        dependencyCheckPublisher()
      }
    }

  }
}