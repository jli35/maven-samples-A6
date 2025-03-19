pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        git(url: 'https://github.com/jli35/maven-samples-A6', branch: 'master')
      }
    }

    stage('run') {
      steps {
        sh 'git bisect start 198644632661c67b6c32f59e9047c11a70685e15 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
        sh 'git bisect run mvn clean test'
      }
    }

  }
  tools {
    maven 'DHT_MVN'
    jdk 'DHT_SENSE'
  }
  post {
    failure {
      script {
        try {
          sh 'git bisect reset'
          sh 'git checkout master'
        } catch (Exception e) {
          echo "Failed to reset: ${e.message}"
        } finally {
          // Optional: Add any cleanup steps here
        }
      }

    }

  }
}