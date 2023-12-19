pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'
        // DOCKER_IMAGE = 'Sample_Web_Application'
    }

    tools {
        maven 'Maven'
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

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

//         stage('Run Docker Container') {
//             steps {
//                 script {
//                     sh "docker run -p 8080:8080 --name your-java-container ${DOCKER_IMAGE}"
//                 }
//             }
//         }

//         stage('Deploy') {
//             steps {
//                 sh "${MAVEN_HOME}/bin/mvn tomcat7:redeploy"
//             }
//         }
//     }

//     post {
//         success {
//             script {
//                 echo 'Build, Docker build, and deployment successful!'
//             }
//         }
//         failure {
//             script {
//                 echo 'Build, Docker build, or deployment failed!'
//             }
//         }
//         always {
//             // Post actions that should run regardless of success or failure
//         }
//     }
// }
