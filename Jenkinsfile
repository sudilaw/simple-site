pipeline {
  agent any

  stages {
    stage('Clone Project') {
      steps {
        git 'https://github.com/sudilaw/09jenkins.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'sudo apt update && sudo apt install -y apache2'
      }
    }

    stage('Check Apache Logs') {
      steps {
        sh 'grep -E "HTTP/1.1\" [45][0-9]{2}" /var/log/apache2/access.log || echo "No errors"'
      }
    }

    stage('Finish') {
      steps {
        echo 'Pipeline complete'
      }
    }
  }
}

