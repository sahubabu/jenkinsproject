pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[credentialsId: 'eae29205-3246-4932-b4bf-6b3600beb14b', url: 'https://github.com/sahubabu/jenkinsproject.git']]
                ])
            }
        }
        stage('build') {
            steps {
                git branch: 'main', credentialsId: 'eae29205-3246-4932-b4bf-6b3600beb14b', url: 'https://github.com/sahubabu/jenkinsproject.git'
                sh 'python3 sample.py'
            }
        }
        stage('deployment') {
            steps {
                echo "DONE"
            }
        }
    }
}
