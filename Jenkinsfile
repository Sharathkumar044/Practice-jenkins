pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'
        SONARQUBE_HOME = '/path/to/sonarqube'
    }

    tools {
        maven 'Maven'
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
                script {
                    def mavenHome = tool 'Maven'
                    def mavenSettings = findFiles(glob: '**/settings.xml')[0]
                    withMaven(maven: mavenHome, mavenSettingsConfig: 'your-settings-config-id') {
                        sh "mvn clean install"
                    }
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQubeScanner'
                    withSonarQubeEnv('YourSonarQubeServer') {
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
