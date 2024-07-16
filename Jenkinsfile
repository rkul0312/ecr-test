pipeline {
    agent any

    environment {
        // Define the environment variables for GIT_ASKPASS
        GIT_ASKPASS = '/usr/local/bin/git-askpass.sh'
        GIT_USERNAME = credentials('rkul0312') // The credential ID for the Git username
        GIT_PASSWORD = credentials('80548ab2-bf53-4428-ba81-af15d276f0e4') // The credential ID for the Git password or token
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Create the GIT_ASKPASS script dynamically
                    sh '''
                    echo '#!/bin/sh' > /usr/local/bin/git-askpass.sh
                    echo 'echo $GIT_PASSWORD' >> /usr/local/bin/git-askpass.sh
                    chmod +x /usr/local/bin/git-askpass.sh
                    '''

                    // Set the GIT_ASKPASS environment variable
                    withEnv(['GIT_ASKPASS=/usr/local/bin/git-askpass.sh']) {
                        // Clone the repository
                        sh 'git clone https://github.com/rkul0312/ecr-test.git'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                // Your build steps go here
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                // Your test steps go here
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                // Your deploy steps go here
                echo 'Deploying...'
            }
        }
    }

    post {
        always {
            // Clean up the GIT_ASKPASS script
            sh 'rm -f /usr/local/bin/git-askpass.sh'
        }
    }
}

