pipeline {
    agent any

    environment {
      PATH = "/usr/local/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'npm install'
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
                sh 'npm build'
                sh '''
                   git config user.name "Antoshef"
                   git config user.email "antoshef21@gmail.com"
                   git checkout dev
                   git merge master
                   git push origin dev
                '''
            }
        }
    }
}