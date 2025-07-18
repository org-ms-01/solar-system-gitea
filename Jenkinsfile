pipeline {
    agent any

    environment {
         MONGO_URI = "mongodb+srv://supercluster.d83jj.mongodb.net/superData"
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }

        stage('Dependency Scanning') {
            parallel {
                stage('Run npm audit') {
                    steps {
                        sh 'npm audit --audit-level=critical'
                    }
                }

                stage('OWASP Dependency Check') {
                    steps {
                        dependencyCheck additionalArguments: '''
                            --scan ./ 
                            --out ./ 
                            --format ALL 
                            --prettyPrint
                        ''',
                        odcInstallation: 'OWASP-Dependency-Check'

                        dependencyCheckPublisher failedTotalCritical: 1, 
                                                 pattern: 'dependency-check-report.html', 
                                                 stopBuild: true
                        junit allowEmptyResults: true, keepProperties: true, testResults: 'dependency-check-junit.xml'
                        publishHTML([allowMissing: true, 
                                     alwaysLinkToLastBuild: true, 
                                     icon: '', 
                                     keepAll: true, 
                                     reportDir: './', 
                                     reportFiles: 'dependency-check-jenkins.html', 
                                     reportName: 'dependency-check HTML Report', 
                                     reportTitles: '', 
                                     useWrapperFileDirectly: true])
                    }
                }
            }
        }
        stage('Unit Testing') {
            steps {
                withCredentials([usernamePassword(credentialsId: '', passwordVariable: 'MONGO_PASSWORD', usernameVariable: 'MONGO_USERNAME')]) {
                    sh 'npm test'
            }
            junit allowEmptyResults: true, keepProperties: true, testResults: 'test.xml'
            }
        }
    }
}
