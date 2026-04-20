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
            -Dsonar.login=sqa_055a7825eaefdf1a40bfea6829c12126e76faf87
            '''
        }
    }
}

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}