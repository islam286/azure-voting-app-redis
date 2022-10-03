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
                    docker images -a
                    """)
                sh(script: """
                   
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    cd ..
                """)
                
            }
        }
      stage('Start test app') {
         steps {
            pwsh(script: """
               #start app line missing!
               ./scripts/test_container.ps1
            """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            pwsh(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            pwsh(script: """
               docker-compose down
            """)
         }
      }
    }
}
