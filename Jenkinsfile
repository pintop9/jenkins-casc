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
                sh 'docker run --rm chuanwen/cowsay -f dragon "I breathe fire and DinD!"'
            }
        }

        stage('motd') {
            steps {
                echo '$(docker logs ${docker ps -alq})'
            }
        }
    }
}