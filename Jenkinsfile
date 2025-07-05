pipeline {
    agent any

    stages {
        stage('Clone'){
            steps {
                git '/home/admin/Documents/flask-ci-local'
            }
        }
   

    stage('Install Dependencies') {
        steps {
            sh 'pip install -r requirements.txt'
        }
    }

    stage('Run Tests') {
        steps {
            sh 'pytest'
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
}
