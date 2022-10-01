pipeline {
    agent any

    stages {
        stage('verify branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
    stages {
        stage('docker build') {
            steps {
                pwsh(script: 'docker images -a')
                pwsh(script: """
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins pipeline .
                    cd ..
                """)
                
            }
        }

    }
}
