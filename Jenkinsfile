pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your GitHub repository
                git 'https://github.com/Sharathkumar044/Practice-jenkins.git'
            }
        }

        stage('Build') {
            steps {
                // Build the Maven project
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }

        stage('Test') {
            steps {
                // Run tests if needed
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (adjust this based on your deployment strategy)
                // Example: Deploy to Tomcat
                sh "${MAVEN_HOME}/bin/mvn tomcat7:redeploy"
            }
        }
    }

    post {
        success {
            // Additional steps to execute on success
            echo 'Build and deployment successful!'
        }
        failure {
            // Additional steps to execute on failure
            echo 'Build or deployment failed!'
        }
    }
}
