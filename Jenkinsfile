pipeline {
    agent any

    stages {
        stage('verify branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }

        stage('docker build') {
            steps {
                sh(script: """
                    sudo docker images -a
                    """)
                sh(script: """
                    sudo /etc/init.d/docker start
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins pipeline .
                    cd ..
                """)
                
            }
        }

    }
}
