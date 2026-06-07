pipeline {
    agent any

    tools {
        nodejs 'Node18'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/optimuswave14/FinTrack.git'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    bat 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                }
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'

                    withSonarQubeEnv('SonarCloud') {

                        bat """
                        "${scannerHome}\\bin\\sonar-scanner.bat" ^
                        -Dsonar.organization=optimuswave14 ^
                        -Dsonar.projectKey=optimuswave14_FinTrack ^
                        -Dsonar.sources=. ^
                        -Dsonar.host.url=https://sonarcloud.io
                        """
                    }
                }
            }
        }

    }
}