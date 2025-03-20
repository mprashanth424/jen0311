pipeline {
    agent any

    environment {
        GO_PATH = "$HOME/go/go/bin"
    }

    stages {
        stage('Clone Repository with Submodules') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/mprashanth424/jen0311.git', credentialsId: 'your-credential-id'
                    sh 'git submodule update --init --recursive'
                }
            }
        }
        stage('Install Go') {
            steps {
                sh '''
                    curl -L -o go.tar.gz https://go.dev/dl/go1.21.0.darwin-amd64.tar.gz
                    mkdir -p $HOME/go
                    tar -C $HOME/go -xzf go.tar.gz
                    chmod +x $HOME/go/go/bin/go
                    export PATH=$HOME/go/go/bin:$PATH
                    echo "Go path set: $PATH"
                    go version
                '''
            }
        }
        stage('Set Up Go Modules') {
            steps {
                sh '''
                    export PATH=$HOME/go/go/bin:$PATH
                    cd workforcepro/backend
                    go mod tidy
                '''
            }
        }
        stage('Build Go Application') {
            steps {
                sh '''
                    export PATH=$HOME/go/go/bin:$PATH
                    cd workforcepro/backend
                    go build -o workforce-app
                '''
            }
        }
        stage('Run Go Application') {
            steps {
                sh '''
                    export PATH=$HOME/go/go/bin:$PATH
           	    cd workforcepro/backend
           	    chmod +x workforce-app  # Ensure the app is executable
           	    nohup ./workforce-app > app.log 2>&1 & echo $! > pid.txt
           	    sleep 3  # Give some time for the app to start
           	    cat app.log  # Show the logs in Jenkins output
                '''
            }
        }
    }
}
