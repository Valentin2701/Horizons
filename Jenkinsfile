pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            steps {
                // Restore .NET dependencies
                bat "dotnet restore Horizons.sln"
            }
        }

        stage('Build') {
            steps {
                // Build the project
                bat "dotnet build Horizons.sln --no-restore"
            }
        }

        stage('Test') {
            steps {
                // Run tests
                bat "dotnet test --no-build --verbosity normal"
            }
        }
    }

    post {
        always {
            // Archive test results or publish logs if needed
            archiveArtifacts artifacts: '**/bin/**/*', allowEmptyArchive: true
        }

        failure {
            // Add actions to take if the build fails
            echo 'Build failed!'
        }

        success {
            // Add actions to take if the build succeeds
            echo 'Build and tests succeeded!'
        }
    }
}
