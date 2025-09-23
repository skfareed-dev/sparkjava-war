pipeline {
    agent { label 'maven' }

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
                scannerHome = tool 'sonarscanner' // name of SonarQube Scanner in Jenkins
            }
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    sh """
                        ${scannerHome}/bin/sonar-scanner \
                          -Dsonar.projectKey=skfareed-dev_sparkjava-war \
                          -Dsonar.sources=src/main/java \
                          -Dsonar.tests= \
                          -Dsonar.host.url=$SONAR_HOST_URL \
                          -Dsonar.login=$SONAR_AUTH_TOKEN
                    """
                }
            }
        }

        stage('Quality Gate Check') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "❌ SonarQube Quality Gate failed: ${qg.status}"
                    } else {
                        echo "✅ Quality Gate passed!"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}