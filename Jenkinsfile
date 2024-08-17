pipeline {
    agent any

    environment {
      PATH = "/Users/antoshef/.local/share/nvm/v22.3.0/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                    nvm use 22.3.0
                    npm install
                '''
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
                    nvm use 22.3.0
                    CI=true npm test
                '''
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