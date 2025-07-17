pipeline {
    agent any

    stages {
        stage('Check Node and NPM Versions') {
            steps {
                echo 'Checking Node.js and npm versions...'
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies (no audit)...'
                sh 'npm install --no-audit'
            }
        }
    }
}
