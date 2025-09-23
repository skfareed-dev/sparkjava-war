pipeline {
    agent {label 'maven'} 

    // stages {
    //     stage('checkout') {
    //         steps {
    //            git branch: 'main', url: 'https://github.com/skfareed-dev/sparkjava-war'
    //         }
    //     }
    // }


    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
            stage('SonarQube analysis') {
    environment {
      scannerHome = tool 'sonarscanner' // This is the name of the SonarQube Scanner installation in Jenkins
    }
    steps{
    withSonarQubeEnv('sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }

        stage('Deploy') {
            steps {
                // Add your deployment steps here
                echo 'Deploying application...'
            }
        }
    }
}
