pipeline {
    agent any
        stages {
            stage ('Checkout') {
                steps {
                    git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
                }
            }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.login=sqp_e2cf9fa3d8f60dff5fd47a56e300c02e757b72e5"
                    }
                }
            }
        }
    }

    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}