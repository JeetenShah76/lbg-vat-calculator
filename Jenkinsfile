pipeline {
  agent any

  stages {
    stage('Checkout') {
        steps {
          // Get some code from a GitHub repository
          git branch: 'main', url: 'https://github.com/JeetenShah76/lbg-vat-calculator.git'
        }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
  stage('Install') {
        steps {
            // Install the ReactJS dependencies
            sh "npm install"
        }
    }
    stage('Test') {
        steps {
          // Run the ReactJS tests
          sh "npm test"
        }
    }
        steps {
            withSonarQubeEnv('sonar-qube-1') {        
              sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES'){
          waitForQualityGate abortPipeline: true
        }
    }
  }
}
}
