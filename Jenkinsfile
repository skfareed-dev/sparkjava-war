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
        stage('Deploy') {
            steps {
                // Add your deployment steps here
                echo 'Deploying application...'
            }
        }
    }
}
