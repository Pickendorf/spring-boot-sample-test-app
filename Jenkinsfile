pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build stage'
        bat(script: 'mvnw -DskipTests clean install', returnStdout: true)
        bat 'echo Fin de build'
      }
    }

    stage('test') {
      parallel {
        stage('test intégration') {
          steps {
            echo 'test d\'intégration'
          }
        }

        stage('test fonctionnel') {
          steps {
            echo 'test fonctionnel'
          }
        }

        stage('smoke test') {
          steps {
            echo 'smoke test'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        echo 'stage deploy'
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}