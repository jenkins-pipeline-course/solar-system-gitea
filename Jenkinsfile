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

        stage('NPM Dependency Audit') {
            steps {
                sh 'npm audit --audit-level=critical'
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '''
                    --scan \'./\'
                    --out \'./\'
                    --format \'ALL\'
                    --prettyPrint''', odcInstallation: 'OWASP-DepCheck-10'

                dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml',
                stopBuild: true

                junit allowEmptyResults: true, stdioRetention: '', testResults: 'dependency-check-junit.xml'

                publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, keepAll: true, reportDir:
                './', reportFiles: 'dependency-check-jenkins.html', reportName: 'Dependency Check HTML
                Report', reportTitles: '', useWrapperFileDirectly: true])
            }
        }  
    }
}