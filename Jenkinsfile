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
                    -Dsonar.login=f78a0bf2dc4540f8a431051627d1a766055419da \
                    -Dsonar.coverage.exclusions=**/database/**,**/dto/**,**/tables/**,**/tests/**,*.txt,*.yml,*.xml,*.env \
                    -Dsonar.pullrequest.branch=${GIT_LOCAL_BRANCH}
                    -Dsonar.pullrequest.key=1 \
                    -Dsonar.pullrequest.base=master"
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