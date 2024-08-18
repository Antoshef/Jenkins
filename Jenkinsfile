pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:$PATH"
    }

    stages {
        stage('Init') {
            steps {
                echo 'Initializing...'
                sh 'npm install'
            }
        }
        stage('Build') {
            when {
                branch 'master'
            }
            steps {
                echo 'Building application...'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'CI=true npm test'
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to dev branch...'
                sh '''
                    git config user.name "Antoshef"
                    git config user.email "antoshef21@gmail.com"
                    git fetch origin
                    git checkout dev || git checkout -b dev
                    rm -rf * .[!.]* || true  # Remove all files and hidden files, excluding .git
                    if [ -d build ]; then
                        cp -r build/* .  # Copy build contents to root of dev branch
                        git add .
                        git commit -m "Deploy build folder to dev branch"
                        git push origin dev
                    else
                        echo "Build directory does not exist. Skipping deployment."
                        exit 1
                    fi
                '''
            }
        }
    }
}