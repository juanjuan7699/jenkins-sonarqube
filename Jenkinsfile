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
						sh 'sonar-scanner.bat -D"sonar.projectKey=OWASP" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login=sqp_613148d1e5490972da5d888b612c6b3943fcc209"'
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
