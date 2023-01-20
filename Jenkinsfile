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
              docker compose up -d
              echo ${env.WORKSPACE}
              sh "chmod 777 ${env.WORKSPACE}"/scripts/test_container.sh
             ./scripts/test_container.sh
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
              docker compose down
              """)
        }
      }
   }
}
