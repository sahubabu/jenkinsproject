pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your Git repository
                git 'https://github.com/yourusername/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                // Build your project (if applicable)
                echo 'Builting the application...'
            }
        }

        stage('Run Python Script') {
            steps {
                // Execute a Python script
                script {
                    try {
                        sh 'python my_python_script.py'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Python script execution failed: ${e.message}")
                    }
                }
            }
        }

        stage('Test') {
            steps {
                // Run tests (if applicable)
                echo 'Testing the application...'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy your application (if applicable)
                echo 'Deploying the application...'
            }
        }
    }

    post {
        success {
            // Actions to take if the pipeline succeeds
            echo 'Pipeline completed successfully!'
        }
        failure {
            // Actions to take if the pipeline fails
            echo 'Pipeline failed! Send a notification.'
        }
    }
}
