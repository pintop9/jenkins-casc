pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
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
                // Pull only if missing (safe + fast)
                sh 'docker pull --pull=never chuanwen/cowsay || true'
            }
        }

        stage('Run Cowsay') {
            steps {
                sh 'docker run --rm chuanwen/cowsay  --name jenkinsdind "Jenkins rocks! Running Docker-in-Docker like a boss!"'
            }
        }

        stage('motd') {
            steps {
                echo '$(docker logs jenkinsdind)'
            }
        }
    }
}