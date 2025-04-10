pipeline {
  agent any

  stages {
    stage('Clone Project') {
      steps {
        git 'https://github.com/sudilaw/simple-site'
      }
    }

    stage('Install Apache') {
      steps {
        sh 'sudo apt update && sudo apt install -y apache2'
      }
    }

    stage('Copy of index.html') {
      steps {
	sh '''
	  sudo cp index.html /var/www/html/index.html
	'''
      }
    }

    stage('Check of site running') {
      steps {
	sh 'curl -I http:localhost'
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

