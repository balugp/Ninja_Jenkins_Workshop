pipeline {
  agent any
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${params.Name}!"
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
        sh 'java -version'
      }
    }
    stage('Testing') {
      failFast true
      parallel {
        stage('Java 7') {
          agent any
          steps {
            sh 'java -version'
            sleep(time: 10, unit: 'SECONDS')
          }
        }
        stage('Java 8') {
          agent any
          steps {
            sh 'java -version'
            sleep(time: 20, unit: 'SECONDS')
          }
        }
      }
    }
  }
  environment {
    MY_NAME = 'Mary'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
}