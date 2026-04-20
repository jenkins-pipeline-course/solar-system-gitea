pipeline {
    agent any
    tools {
        nodejs 'node-25.9.0'   // must match the name you set in Jenkins Tools
    }
    stages {
        stage('Node Version') {
            steps {
                sh 'npm install --no-audit'
            }
        }
    }

    stages {
        stage('NPM Dependency Audit') {
            steps {
                sh 'npm audit --audit-level=critical'
            }
        }
    }
}