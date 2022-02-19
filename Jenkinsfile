pipeline {
  agent any
  stages {
    stage('Fluffy Build') {
      parallel {
        stage('Fluffy Build') {
          steps {
            sh './jenkins/build.sh'
          }
        }

        stage('') {
          steps {
            archiveArtifacts 'target/*.jar'
          }
        }

      }
    }

    stage('Fluffy Test') {
      parallel {
        stage('Fluffy Test') {
          steps {
            sh './jenkins/test-all.sh'
          }
        }

        stage('') {
          steps {
            junit 'target/**/TEST*.xml'
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