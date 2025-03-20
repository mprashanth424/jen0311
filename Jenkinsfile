pipeline {
    agent any

    stages {
        stage('Clone Repository with Submodules') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/mprashanth424/jen0311.git', credentialsId: 'your-credential-id'
                    sh 'git submodule update --init --recursive'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
                sh 'pip3 install -r workforcepro/requirements.txt'  // Install dependencies from submodule
            }
        }
        stage('Run Flask App') {
            steps {
                sh 'nohup python3 workforcepro/app.py &'
            }
        }
    }
}
