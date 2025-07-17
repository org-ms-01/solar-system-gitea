pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }

        stage('Run npm audit') {
            steps {
                sh 'npm audit --audit-level=critical'
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '''
                    --scan . 
                    --out ./ 
                    --format ALL 
                    --prettyPrint
                ''', 
                dcInstallation: 'OWASP-DepCheck-10'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/dependency-check-report.*', fingerprint: true
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
