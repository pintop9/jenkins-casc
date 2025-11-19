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
                sh 'docker pull --pull=never midget/cowsay'
        }

        stage('Run Confluence Container') {
            steps {

                sh 'docker run --rm midget/cowsay Jenkins rocks! and currently runinng docker in docker!'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "You can now access Confluence on http://localhost:8090"'
            }
        }
    }
}
}