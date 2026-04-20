pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                sh 'git clone https://github.com/MoDiouf/Devops-Train.git'
            }
        }
        stage('Install Dependencies'){
            steps{
                sh 'npm install'
            }
        }
        stage('Build'){
            steps{
                sh 'npm run build'
            }
        }
        stage('Test'){
            steps{
                sh 'npm run test'
            }
        }
    }
}