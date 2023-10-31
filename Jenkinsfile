pipeline {
    agent any

    parameters {
        string(name: 'GIT_REPO_URL', description: 'Git repository URL', defaultValue: 'https://github.com/sahubabu/jenkinsproject.git')
        string(name: 'GIT_CREDENTIALS_ID', description: 'Git credentials ID', defaultValue: 'eae29205-3246-4932-b4bf-6b3600beb14b')
        string(name: 'PYTHON_SCRIPT', description: 'Name of the Python script', defaultValue: 'sample.py')
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
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
                    build job: 'downstream-job', parameters: [string(name: 'PYTHON_SCRIPT', value: "${params.PYTHON_SCRIPT}")]
                }
                failure {
                    step([$class: 'Mailer',
                        notifyEveryUnstableBuild: true,
                        recipients: 'pavan.py446@gmail.com',
                        sendToIndividuals: true])
                }
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
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Send a notification.'
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: 'pavan.py446@gmail.com',
                sendToIndividuals: true])
        }
    }
}
