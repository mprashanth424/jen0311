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
        stage('Install Go') {
    steps {
        sh '''
            curl -L -o go.tar.gz https://go.dev/dl/go1.21.0.darwin-amd64.tar.gz
            mkdir -p $HOME/go
            tar -C $HOME/go -xzf go.tar.gz
            chmod +x $HOME/go/go/bin/go
            export PATH=$HOME/go/go/bin:$PATH
            echo "export PATH=$HOME/go/go/bin:$PATH" >> $HOME/.bashrc
            echo "export PATH=$HOME/go/go/bin:$PATH" >> $HOME/.bash_profile
            source $HOME/.bash_profile
            go version
        '''
    }
}
        stage('Set Up Go Modules') {
            steps {
                sh 'cd workforcepro/backend && go mod tidy'
            }
        }
        stage('Build Go Application') {
            steps {
                sh 'cd workforcepro/backend && go build -o workforce-app'
            }
        }
        stage('Run Go Application') {
            steps {
                sh 'cd workforcepro/backend && nohup ./workforce-app &'
            }
        }
    }
}
