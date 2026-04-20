pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }

        stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('sonar') {
            sh '''
            npx sonar-scanner \
            -Dsonar.projectKey=my-node-project \
            -Dsonar.sources=src \
            -Dsonar.host.url=http://sonarqube:9000 \
            -Dsonar.exclusions=**/node_modules/**,**/*.spec.ts \
            -Dsonar.javascript.node.max_old_space_size=4096
            '''
        }
    }
}


        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}