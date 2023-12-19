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
                    // Assuming Maven is available in the PATH or you've configured the tool installation in Jenkins
                    sh 'mvn clean package'
                }
            }
        }

        // Add more stages as needed for deployment, testing, etc.

    }

    post {
        always {
            // Cleanup or additional actions after the pipeline completes
        }
    }
}
