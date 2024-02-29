pipeline {
  agent any

  parameters {
    string(name: 'SPEC', defaultValue: 'cypress/e2e/1-getting-started/**', description: 'Enter the path of script to exec')
    choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'], description: 'Choice the browser')
  }
  options {
    ansiColor('xterm')
  }
  stages {
    // first stage installs node dependencies and Cypress binary
    stage('build') {
      steps {
        echo 'building the app'
        bat 'node ./scripts/start.js'
      }

    }
    stage('testing') {
      steps {
        bat 'npm i'
        bat 'npx cypress run --browser ${BROWSER} --spec ${SPEC}'
      }

    }

    stage('deploy') {
      steps {
        echo 'Deploy the application'
      }

    }

  }

  post {
    // shutdown the server running in the background
    always {
      echo 'Stopping local server'
      bat 'taskkill /IM http-server /F'

    }
  }

}