pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('List files') {
      steps {
        script {
          if (isUnix()) {
            sh 'ls -la'
          } else {
            bat 'dir'
          }
        }
      }
    }

    stage('Run ZipGo script') {
      steps {
        script {
          if (isUnix()) {
            // make sure script is executable, then run it
            sh 'chmod +x zipgo.sh || true'
            sh './zipgo.sh'
          } else {
            // Prefer a Windows batch file if available. If not, try to run bash if installed.
            // We'll run zipgo.bat if present; otherwise attempt bash (Git Bash) as fallback.
            bat '''
            if exist zipgo.bat (
                echo Running zipgo.bat
                zipgo.bat
            ) else (
                echo zipgo.bat not found, attempting to run via bash (requires Git Bash)
                bash zipgo.sh
            )
            '''
          }
        }
      }
    }
  }
  post {
    always {
      echo "Pipeline finished with result: ${currentBuild.currentResult}"
    }
  }
}
