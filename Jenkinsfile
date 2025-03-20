pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/mprashanth424/jen0311.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '/opt/anaconda3/bin/pip3 install -r requirements.txt'
            }
        }
        stage('Run Flask App') {
            steps {
                sh 'nohup python3 app.py &'
            }
        }
    }
}