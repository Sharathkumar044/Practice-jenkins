pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'
        SONARQUBE_HOME = '/path/to/sonarqube' // Provide the path to your SonarQube Scanner installation
    }

    tools {
        maven 'Maven'
        // Add SonarQube Scanner installation as a tool
        // Install SonarQube Scanner tool in Jenkins and reference it here
        sonarqube 'SonarQubeScanner'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Sharathkumar044/Practice-jenkins.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }

    post {
        always {
            // Cleanup or additional steps to be executed after all stages
        }
    }
}
