pipeline {
    agent any // Specifies that the pipeline can run on any available agent

     options {
        // Add timestamps to logs
        timestamps()
        // Build discarder (optional)
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

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
    stages {
        stage('pull public docker image') {
            steps {
                sh 'docker pull atlassian/confluence:8.9.7' 
            }
        }
        stage('run confluence container') {
            steps {
                sh 'docker run -d -p 8090:8090 --name="confluence" atlassian/confluence:8.9.7' 
               
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo you can now access confluence on http://localhost:8090'
            }
        }
}
    }
}