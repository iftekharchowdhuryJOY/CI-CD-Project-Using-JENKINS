pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/iftekharchowdhuryJOY/CI-CD-Project-Using-JENKINS.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    export PYTHONPATH=$PWD
                    pytest
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-ci-app .'
            }
        }

        stage('Run App in Docker') {
            steps {
                sh 'docker stop flask-ci-app || true && docker rm flask-ci-app || true'
                sh 'docker run -d --name flask-ci-app -p 5000:5000 flask-ci-app'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished running.'
        }
        success {
            echo '✅ Pipeline succeeded!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
