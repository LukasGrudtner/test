pipeline {
    agent any
    stages {
        stage ('Sonar Analysis') {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    sh "${scannerHome}/bin/sonar-scanner \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=f78a0bf2dc4540f8a431051627d1a766055419da \
                    -Dsonar.pullrequest.branch=dev \
                    -Dsonar.pullrequest.key=3"
                }
            }
        }
    }
}