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
                    -Dsonar.branch.name=${GIT_LOCAL_BRANCH} \
                    -Dsonar.projectKey=test \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.login=8eeb8c92b9e2ac589ae7990d9c566b0b9efe5f47 \
                    -Dsonar.coverage.exclusions=**/database/**,**/dto/**,**/tables/**,**/tests/**,*.txt,*.yml,*.xml,*.env"
                }
            }
        }
        stage ('Quality Gate') {
            steps {
                sleep(5)
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
