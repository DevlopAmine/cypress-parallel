pipeline {
  agent any

  //parameters {
  //string(name: 'SPEC', defaultValue: 'cypress/e2e/2-advanced-examples/**.cy.js', description: 'Enter the path of script to exec')
  //choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'], description: 'Choice the browser')
  // }
  environment {
    CYPRESS_RECORD_KEY = '46fec6e6-3734-4e43-a577-b74c4c88483e'
  }
  options {
    ansiColor('xterm')
  }
  stages {
    // first stage installs node dependencies and Cypress binary
    stage('build') {

      steps {
        // Check if node_modules exists

        script {

        // Install dependencies using npm or npm ci (recommended)
        echo 'Installing dependencies using npm i'
        bat 'npm i' // Or sh 'npm install'
        }
        echo 'record key below'
        echo '%CYPRESS_RECORD_KEY%'

      }

    }
    stage('testing') {

      //echo 'record key: ${Cypress.env("CYPRESS_RECORD_KEY")}'
      //bat 'npx cypress run --record --key %CYPRESS_RECORD_KEY% --spec %SPEC% --group Windows/Chrome chrome'
      //bat 'npx cypress run --browser %BROWSER% --spec %SPEC%'
      //bat 'npx cypress run --browser chrome'

      
        // start several test jobs in parallel, and they all
        // will use Cypress Cloud to load balance any found spec files
/*         stage('run on chrome') {
          steps {
            echo "Running build  ${env.BUILD_ID}"
            bat "npm run e2e:record:chrome"
          }
        }

        // second tester runs the same command
        stage('run on edge') {
          steps {
            echo "Running build  ${env.BUILD_ID}"
            bat "npm run e2e:record:edge"
          }
        }

        stage('run on Parallel') {
          steps {
            echo "Running build  ${env.BUILD_ID}"
            bat "npm run e2e:record:parallel"
          }
        } */

    parallel {
        stage('Group 1-getting-started/') {
          steps {
            echo "Running build  ${env.BUILD_NUMBER}"
            bat 'cypress run --record --group getStarted --spec "cypress/e2e/1-getting-started/*"'
            
          }
        }

         stage('Group 2-advanced-examples') {
          steps {
            echo "Running build  ${env.BUILD_NUMBER}"
            bat 'cypress run --record --group advancedExamp --spec "cypress/e2e/2-advanced-examples/*"'
          }
        }
    }

    }
    stage('deploy') {
      steps {
        echo 'Deploy the application'
      }

    }

  }

  post {
    always {

      // publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
      echo 'Stopping local server'
      //sh 'pkill -f http-server'
      //bat 'taskkill /IM http-server /F'

    }
  }

}