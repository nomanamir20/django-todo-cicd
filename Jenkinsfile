pipeline {
  agent any
  options {
    timeout(time: 10, unit: 'MINUTES')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t todo .'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run --rm todo python manage.py check'
      }
    }
    stage('Deploy') {
      steps {
        sh 'docker rm -f todo_container || true'
        sh 'docker run -d -p 8000:8000 --name todo_container todo'
      }
    }
  }
}
