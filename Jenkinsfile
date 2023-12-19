pipeline {
    agent {
        label 'SlaveAgent'
    }

    stages {
        stage('Checkout') {
            steps {
                // Replace the repository URL with your actual Git repository URL
                checkout([$class: 'GitSCM', branches: [[name: 'feature/sampleapp']], userRemoteConfigs: [[url: 'https://github.com/Sharathkumar044/Practice-jenkins.git']]])
            }
        }
    }
}
