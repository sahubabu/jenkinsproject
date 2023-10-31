pipeline {
    agent any

    parameters {
        string(name: 'GIT_REPO_URL', description: 'Git repository URL', defaultValue: 'https://github.com/sahubabu/jenkinsproject.git')
        string(name: 'GIT_CREDENTIALS_ID', description: 'Git credentials ID', defaultValue: 'eae29205-3246-4932-b4bf-6b3600beb14b')
        string(name: 'PYTHON_SCRIPT', description: 'Name of the Python script', defaultValue: 'sample.py')
        string(name: 'EMAIL_RECIPIENTS', description: 'Email recipients (comma-separated)', defaultValue: 'ashok.pydev.com')
    }

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[credentialsId: "${params.GIT_CREDENTIALS_ID}", url: "${params.GIT_REPO_URL}"]]
                ])
            }
        }
        stage('build') {
            steps {
                git branch: 'main', credentialsId: "${params.GIT_CREDENTIALS_ID}", url: "${params.GIT_REPO_URL}"
                sh "python3 ${params.PYTHON_SCRIPT}"
            }
        }
        stage('deployment') {
            steps {
                echo "DONE"
            }
        }
    }

    post {
        success {
            script {
                emailext (
                    to: "${params.EMAIL_RECIPIENTS}",
                    subject: "Jenkins Pipeline Successful",
                    body: "The Jenkins pipeline has completed successfully."
                )
            }
        }
        failure {
            script {
                emailext (
                    to: "${params.EMAIL_RECIPIENTS}",
                    subject: "Jenkins Pipeline Failed",
                    body: "The Jenkins pipeline has failed. Please review the logs for details."
                )
            }
            echo 'Pipeline failed! Send a notification.'
        }
    }
}
