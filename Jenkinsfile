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
                    sh 'mvn clean package'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
    }

    post {
        success {
            script {
                echo 'Build successful! Sending success notification...'
                try {
                    emailext (
                        subject: "Pipeline Successful: \${currentBuild.fullDisplayName}",
                        body: "The pipeline \${currentBuild.fullDisplayName} has completed successfully. No issues found.",
                        to: "jagarapumutyalun@gmail.com",
                        attachLog: true,
                    )
                } catch (Exception e) {
                    echo "Error sending success email: ${e.message}"
                }
            }
        }

        failure {
            script {
                echo 'Build failed! Sending failure notification...'
                try {
                    emailext (
                        subject: "Pipeline Failed: \${currentBuild.fullDisplayName}",
                        body: "The pipeline \${currentBuild.fullDisplayName} has failed. Please investigate and take necessary actions.",
                        to: "jagarapumutyalun@gmail.com",
                        attachLog: true,
                    )
                } catch (Exception e) {
                    echo "Error sending failure email: ${e.message}"
                }
            }
        }
    }
}
