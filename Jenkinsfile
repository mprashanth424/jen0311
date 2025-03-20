pipeline {
    agent {
        docker {
            image 'python:3.9'
        }
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/mprashanth424/jen0311.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Run Flask App') {
            steps {
                sh 'nohup python app.py &'
            }
        }
    }
}