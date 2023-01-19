pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Build Docker') {
        steps{
            sh(script: 'docker images -a')
            sh(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
             """ )
        }
      }
      stage('Start test app') {
        steps {
           sh(script: """
              docker-compose up -d
              ./scripts/test_container.ps1
           """)
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
