pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout https://github.com/Valentin2701/Horizons
            }
        }

        stage('Restore Dependencies') {
            steps {
                // Restore .NET dependencies
                dotnet restore
            }
        }

        stage('Build') {
            steps {
                // Build the project
                dotnet build --no-restore
            }
        }

        stage('Test') {
            steps {
                // Run tests
                dotnet test --no-build --verbosity normal
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
