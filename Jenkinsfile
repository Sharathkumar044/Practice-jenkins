pipeline {
    agent {
        label 'SlaveAgent'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'feature/sampleapp']], userRemoteConfigs: [[url: 'https://github.com/Sharathkumar044/Practice-jenkins.git']]])
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        sh 'mvn clean package'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Build failed: ${e.message}")
                    }
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    try {
                        withSonarQubeEnv('SonarQube') {
                            sh 'mvn sonar:sonar'
                        }
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("SonarQube analysis failed: ${e.message}")
                    }
                }
            }
        }

        // Add more stages as needed for deployment, testing, etc.

    }

    post {
        always {
            emailext (
                subject: "Pipeline Result: \${currentBuild.fullDisplayName}",
                body: "The pipeline \${currentBuild.fullDisplayName} has finished. Result: \${currentBuild.result}",
                to: "jagarapumutyalun@example.com",
            )
        }
    }
}
