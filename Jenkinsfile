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

        stage('Post Actions') {
            steps {
                script {
                    echo 'Build successful! Sending success notification...'
                    try {
                        emailext (
                            subject: "Pipeline Successful: \${currentBuild.fullDisplayName}",
                            body: "The pipeline \${currentBuild.fullDisplayName} has completed successfully. No issues found.",
                            to: "jagarapumutyalun@gmail.com",
                            attachLog: true,
                            mimeType: 'text/html',
                            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                            presendScript: '''\
                                import javax.mail.Message.RecipientType
                                def auth = 'SMTP:banalasharath1@gmail.com'
                                def mailProps = [
                                    'mail.smtp.auth': 'true',
                                    'mail.smtp.starttls.enable': 'true',
                                    'mail.smtp.host': 'smtp.gmail.com',
                                    'mail.smtp.port': '587',
                                    'mail.smtp.user': 'banalasharath1@gmail.com'
                                ]
                                def userCreds = com.cloudbees.plugins.credentials.CredentialsProvider.findCredentialById(auth, com.cloudbees.plugins.credentials.Credentials.class, null)
                                if (userCreds != null) {
                                    def user = userCreds.username
                                    def pass = userCreds.password
                                    msg.setFrom(user)
                                    msg.addRecipients(RecipientType.TO, "jagarapumutyalun@gmail.com")
                                    msg.setSubject("Pipeline Successful: \${currentBuild.fullDisplayName}")
                                    msg.setText("The pipeline \${currentBuild.fullDisplayName} has completed successfully. No issues found.")
                                    transport.send(msg, user, pass)
                                } else {
                                    throw new Exception("Could not find credentials for $auth")
                                }
                            '''
                        )
                    } catch (Exception e) {
                        echo "Error sending success email: ${e.message}"
                    }
                }
            }
        }
    }
}
