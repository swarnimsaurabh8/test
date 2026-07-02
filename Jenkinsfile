pipeline {
    agent any

    environment {
        PROJECT = "WebApplication5/WebApplication5.csproj"
        PUBLISH_DIR = "D:\\publish"
        APPPOOL = "TestNew"      // Change if your app pool has a different name
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/swarnimsaurabh8/test.git'
            }
        }

        stage('Restore') {
            steps {
                bat "dotnet restore %PROJECT%"
            }
        }

        stage('Build') {
            steps {
                bat "dotnet build %PROJECT% --configuration Release --no-restore"
            }
        }

        stage('Stop IIS') {
            steps {
                bat '''
                C:\\Windows\\System32\\inetsrv\\appcmd stop apppool /apppool.name:"%APPPOOL%"
                '''
            }
        }

        stage('Publish') {
            steps {
                bat "dotnet publish %PROJECT% -c Release -o %PUBLISH_DIR% --no-build"
            }
        }

        stage('Start IIS') {
            steps {
                bat '''
                C:\\Windows\\System32\\inetsrv\\appcmd start apppool /apppool.name:"%APPPOOL%"
                '''
            }
        }
    }

    post {

        success {
            echo '======================================='
            echo ' Build & Deployment Successful'
            echo '======================================='
        }

        failure {
            echo '======================================='
            echo ' Build or Deployment Failed'
            echo '======================================='
        }
    }
}
