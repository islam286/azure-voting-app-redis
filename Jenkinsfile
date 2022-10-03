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
            sh(script: """
               docker-compose up -d
               ./scripts/test_container.sh
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
            sh(script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            sh(script: """
               docker-compose down
            """)
         }
      }
    }
    
}
