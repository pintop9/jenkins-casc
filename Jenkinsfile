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
                sh 'docker pull --pull=never atlassian/confluence:8.9.7 || true'
            }
        }

        stage('Run Confluence Container') {
            steps {
                sh '''
                   docker rm -f confluence || true
                '''
                sh 'docker run -d -p 8090:8090 -p 8091:8091 --name="confluence" atlassian/confluence:8.9.7'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "You can now access Confluence on http://localhost:8090"'
            }
        }
    }
}
