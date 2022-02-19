pipeline {
  agent any
  stages {
    stage('Fluffy Build') {
      steps {
        sh './jenkins/build.sh'
        archiveArtifacts 'target/*.jar'
      }
    }

    stage('Fluffy Test') {
      parallel {
        stage('Backend') {
          steps {
            sh './jenkins/test-backend.sh'
            junit(testResults: 'target/surefire-reports/**/TEST*.xml', skipPublishingChecks: true)
          }
        }

        stage('Frontend') {
          steps {
            sh './jenkins/test-frontend.sh'
            junit(testResults: 'target/test-results/**/TEST*.xml', skipPublishingChecks: true)
          }
        }

        stage('Performance') {
          steps {
            sh './jenkins/test-performance.sh'
          }
        }

        stage('Static') {
          steps {
            sh './jenkins/test-static.sh'
          }
        }

      }
    }

    stage('Fluffy Deploy') {
      steps {
        sh './jenkins/deploy.sh staging'
      }
    }

  }
}