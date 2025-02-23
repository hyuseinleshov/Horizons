pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0.x'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'feature-ci-pipeline', url: 'https://github.com/hyuseinleshov/Horizons.git'
            }
        }

        stage('Setup .NET') {
            steps {
                bat 'dotnet --version'
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build Application') {
            steps {
                bat 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Tests completed successfully!'
        }
        failure {
            echo '❌ Build or Tests failed!'
        }
    }
}