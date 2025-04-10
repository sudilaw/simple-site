pipeline {
  agent any

  stages {
    stage('Install Apache') {
      steps {
        sh '''
          sudo apt update
          sudo apt install -y apache2
          sudo systemctl start apache2
          sudo systemctl enable apache2
        '''
      }
    }

    stage('Deploy index.html') {
      steps {
        sh '''
          sudo cp index.html /var/www/html/index.html
        '''
      }
    }

    stage('Logs check-up') {
      steps {
        sh '''
          echo "Error types: 4xx и 5xx in logs Apache:"
          sudo grep -E "HTTP/1.[01]\" [45][0-9]{2}" /var/log/apache2/access.log || echo "Нет ошибок"
        '''
      }
    }
  }

  post {
    success {
      echo '> Apache is setted up, site is on and up-to-date'
    }
    failure {
      echo '> Something went wrong... Again... Check pipeline.'
    }
  }
}