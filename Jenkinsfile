pipeline {
    agent any

    environment {
      PATH = "/Users/antoshef/.local/share/nvm/v22.3.0/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                sh 'CI=true npm test'
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}