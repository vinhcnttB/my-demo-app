pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "C:\\Windows\\Temp"
        SOLUTION_PATH   = "MyDemoApp.sln"
        PUBLISH_DIR     = "publish"
    }

    stages {
        stage("Checkout") {
            steps {
                echo "Dang ket noi va lay code tu GitHub..."
                checkout scm
            }
        }

        stage("Restore") {
            steps {
                echo "Dang restore NuGet packages..."
                bat "dotnet restore ${SOLUTION_PATH}"
            }
        }

        stage("Build") {
            steps {
                echo "Dang build solution..."
                bat "dotnet build ${SOLUTION_PATH} --configuration Release --no-restore"
            }
        }

        stage("Test") {
            steps {
                echo "Dang chay unit tests..."
                bat "dotnet test ${SOLUTION_PATH} --configuration Release --no-build --verbosity normal"
            }
            post {
                always {
                    echo "Ket qua test da hoan thanh"
                }
            }
        }

        stage("Publish") {
            steps {
                echo "Dang publish ung dung..."
                bat "dotnet publish MyDemoApp.API\\MyDemoApp.API.csproj --configuration Release --output ${PUBLISH_DIR}"
            }
        }
    }

    post {
        success {
            echo "Pipeline THANH CONG! Ung dung da duoc build va publish."
        }
        failure {
            echo "Pipeline THAT BAI! Kiem tra log de biet loi."
        }
    }
}