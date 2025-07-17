pipeline {
    agent any

    stages {
        stage('Check Node and NPM Versions') {
            steps {
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }

        stage('Audit for Critical Vulnerabilities') {
            steps {
                echo 'Running npm audit for critical vulnerabilities...'
                sh 'npm audit --audit-level=critical'
            }
        }
    }
}
