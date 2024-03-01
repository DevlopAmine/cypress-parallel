pipeline {
  agent any

  parameters {
    string(name: 'SPEC', defaultValue: 'cypress/e2e/2-advanced-examples/actions.cy.js', description: 'Enter the path of script to exec')
    choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'], description: 'Choice the browser')
  }
  stages {
    // first stage installs node dependencies and Cypress binary
    stage('build') {
      steps {
        echo 'building the app'
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