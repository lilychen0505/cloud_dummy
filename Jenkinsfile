pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube-9.9.2') {
                    script {
                        def sonarScannerHome = tool 'SonarQubeScanner'
                        sh """
                            ${sonarScannerHome}/bin/sonar-scanner \
                            -Dsonar.login=admin \
                            -Dsonar.password=admin
                        """
                    }
                }
            }
        }

        stage('Results') {
            steps {
                echo 'View SonarQube analysis results: http://35.237.243.128:9000/projects'
            }
        }
    }
}
