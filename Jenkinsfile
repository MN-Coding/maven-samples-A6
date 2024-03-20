pipeline {
  agent any
  tools { 
      maven 'DHT_MVN' 
      jdk 'DHT_SENSE' 
  }
  stages {
    stage('check out') {
      steps {
        git(url: 'https://github.com/MN-Coding/maven-samples-A6', branch: 'master')
      }
    }

    stage('run') {
      steps {
        sh 'git bisect start aa3ab90d6cd0bc0a3f17f9412c729889be3a0339 c694c1f295dec4c158d28b0b87d218e24f244f9f'
        sh 'git bisect run mvn clean test'
      }
    }

  }
post {
        failure {
            script {
                try {
                    sh 'git checkout -'
                } catch (Exception e) {
                    echo "Failed to uncheckout the branch: ${e.message}"
                } finally {
                    // Optional: Add any cleanup steps here
                }
            }
        }
    }
  
}
