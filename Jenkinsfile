pipeline {
    agent any

    tools {
        nodejs 'node20'
    }

    environment {
        FIREBASE_TOKEN = credentials('Serverless-Deploy')
    }

    stages {
        stage('Clone') {
            steps {
                echo "Cloning repo....."
                git branch: 'main', url: 'https://github.com/jarntae/server_less.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('frontend') {
                    echo "Installing node modules..."
                    sh 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                dir('frontend') {  // <--- แก้ตรงนี้
                    echo "Building project..."
                    sh 'npx vite build'
                }
            }
        }

        stage('Deploy') {
            steps {
                dir('frontend') {  // <--- แก้ตรงนี้
                    echo "Deploying to Firebase....."
                    sh 'npx firebase deploy --only hosting --token=$FIREBASE_TOKEN'
                }
            }
        }
    }
}
