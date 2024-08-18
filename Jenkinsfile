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
                   rm -rf * .[!.]* || true
                   cp -r build/*
                   git add .
                   git commit -m "Deploy build folder to dev branch"
                   git push origin dev
                '''
            }
        }
    }
}