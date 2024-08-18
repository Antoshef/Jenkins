pipeline {
    agent any

    environment {
      PATH = "/usr/local/bin:$PATH"
    }

    stages {
        stage('Init') {
            steps {
                echo 'Building..'
                sh 'npm install'
            }
        }
        stage('Build') {
          when {
            branch 'master'
          }
          steps {
            sh 'npm run build'
          }
        }
        stage('Test') {
            steps {
                sh 'CI=true npm test'
                echo 'Testing..'
            }
        }
        stage('Deploy') {
          when {
            branch 'master'
          }
            steps {
                echo 'Deploying to dev branch'
                sh '''
                   git config user.name "Antoshef"
                   git config user.email "antoshef21@gmail.com"
                   git fetch origin
                   git checkout dev || git checkout -b dev
                   git checkout -B master origin/master
                   git merge master
                   git push origin dev
                '''
            }
        }
    }
}