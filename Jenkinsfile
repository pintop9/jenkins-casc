pipeline {
    agent any // Pipeline runs on any available agent

    stages {
        stage('Clean Workspace') {
            steps {
                // Delete everything in workspace at start
                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Pull Public Docker Image') {
            steps {
                sh 'docker pull atlassian/confluence:8.9.7'
            }
        }

        stage('Run Confluence Container') {
            steps {
                sh 'docker run -d -p 8090:8090 --name="confluence" atlassian/confluence:8.9.7'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "You can now access Confluence on http://localhost:8090"'
            }
        }
    }
}
