pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build stage'
        bat(script: 'mvnw -DskipTests clean install', returnStdout: true)
        bat 'echo Fin de build'
        bat(script: 'docker build -t testapp:latest', label: 'Docker build', returnStatus: true)
      }
    }

    stage('test') {
      parallel {
        stage('test intégration') {
          steps {
            echo 'test d\'intégration'
            bat 'mvnw -Dtest=com.example.testingweb.integration.** test'
            bat 'echo test integration'
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
        junit '**/target/surefire-reports/TEST-*.xml'
        bat(script: 'docker run -p 3030:8080 testapp:latest', label: 'Docker run', returnStatus: true)
        bat 'echo Application deployee sur le port 3030'
      }
    }

  }
  tools {
    maven 'maven 3.9'
    jdk 'java 11'
  }
}