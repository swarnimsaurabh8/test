pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/swarnimsaurabh8/test.git'
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Publish') {
            steps {
                bat 'dotnet publish -c Release -o D:\\publish'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                xcopy D:\\publish' /E /Y
                '''
            }
        }
    }
}
