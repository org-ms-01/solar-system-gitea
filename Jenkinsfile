pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }

        stage('Dependency Scanning') {
            parallel {
                //stage('Run npm audit') {
                 //   steps {
                //        sh 'npm audit --audit-level=critical'
                //    }
               // }

                stage('OWASP Dependency Check') {
                    steps {
                        dependencyCheck additionalArguments: '''
                            --scan ./ 
                            --out ./ 
                            --format ALL 
                            --prettyPrint
                        ''', 
                        odcInstallation: 'OWASP-DepCheck-10'
                    }
                }
            }
        }
    }
}
