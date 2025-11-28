pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        // Jenkins will automatically checkout pipeline scm
        checkout scm
      }
    }
    stage('List files') {
      steps {
        sh 'ls -la'
      }
    }
    stage('Run ZipGo script') {
      steps {
        sh './zipgo.sh'
      }
    }
  }
}
