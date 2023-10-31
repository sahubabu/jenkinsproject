pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from your Git repository using credentials
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']], // Change to the desired branch
                        userRemoteConfigs: [[url: 'https://github.com/sahubabu/jenkinsproject.git']],
                        credentialsId: 'eae29205-3246-4932-b4bf-6b3600beb14b // Replace with your Git credential ID
                    ])
                }
            }
        }

        stage('Find Jenkinsfile') {
            steps {
                // Locate and execute the Jenkinsfile in the repository
                script {
                    def found = fileExists('Jenkinsfile')
                    if (found) {
                        echo 'Found Jenkinsfile in the repository.'
                        load 'Jenkinsfile' // Execute the Jenkinsfile
                    } else {
                        error 'Jenkinsfile not found in the repository.'
                    }
                }
            }
        }

        stage('Run Python Script') {
            steps {
                // Execute a Python script from the repository
                script {
                    try {
                        sh 'python sample.py' // Replace with the actual Python script name
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error("Python script execution failed: ${e.message}")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Send a notification.'
        }
    }
}
