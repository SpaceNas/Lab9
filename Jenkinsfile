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
                    sh "sonar-scanner.bat -D'sonar.projectKey=OWASP' -D'sonar.sources=.' -D'sonar.host.url=http://localhost:9000' -D'sonar.login=sqp_e2cf9fa3d8f60dff5fd47a56e300c02e757b72e5'"
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