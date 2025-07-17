pipeline {
    agent any

    stages {
        stage('Check Node and NPM Versions') {
            steps {
                script {
                    echo 'Checking Node.js version...'
                    sh 'node -v'
                    
                    echo 'Checking npm version...'
                    sh 'npm -v'
                }
            }
        }
    }
}
