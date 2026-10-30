pipeline {
    agent any
 
    options {
        timestamps()
    }
 
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Check Docker') {
            steps {
                bat 'docker --version'
                bat 'docker compose version'
            }
        }
 
        stage('Validate Compose') {
            steps {
                bat 'docker compose config'
            }
        }
 
        stage('Build and Deploy') {
            steps {
                bat 'docker compose up -d --build'
            }
        }
 
        stage('Verify Containers') {
            steps {
                bat 'docker compose ps'
                bat 'docker compose logs --tail=80 app'
            }
        }
 
        stage('HTTP Health Check') {
            steps {
bat 'curl.exe --fail --silent --show-error http://localhost:8080'
            }
        }
    }
 
    post {
        success {
            echo 'SUCCESS: Laravel deployment completed.'
        }
        failure {
            echo 'FAILED: Check the stage logs and Docker container logs.'
        }
    }
}
