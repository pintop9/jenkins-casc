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

        stage('Victory Moo') {
            steps {
                 sh 'docker run --rm rancher/cowsay "Jenkins rocks! Running Docker-in-Docker like a boss!"'
             }
    }

    }
}