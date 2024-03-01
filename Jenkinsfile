pipeline {
  agent any

  parameters {
    string(name: 'SPEC', defaultValue: 'cypress/e2e/2-advanced-examples/actions.cy.js', description: 'Enter the path of script to exec')
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
      }

    }
    stage('testing') {
      steps {
        bat 'npm i'
        echo 'record key: %Cypress.env("CYPRESS_RECORD_KEY")%'
        bat 'npx cypress run --record --key=%Cypress.env("CYPRESS_RECORD_KEY")%  --spec %SPEC%'
        //bat 'npx cypress run --browser %BROWSER% --spec %SPEC%'
        //bat 'npx cypress run --browser chrome'
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

      publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
      echo 'Stopping local server'
      //sh 'pkill -f http-server'
      //bat 'taskkill /IM http-server /F'

    }
  }

}