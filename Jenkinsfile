pipeline {
  agent any

  environment {
    COMPOSE_CMD = "docker compose -f docker-compose.yml --env-file .env"
  }

  stages {
    stage('Clone') {
      steps {
        checkout scm
      }
    }

    stage('Stop containers') {
      steps {
        sh "${COMPOSE_CMD} down"
      }
    }

    stage('Build') {
      steps {
        sh "${COMPOSE_CMD} build"
      }
    }

    stage('Deploy') {
      steps {
        sh "${COMPOSE_CMD} up -d"
      }
    }

    stage('Check') {
      steps {
        sh "docker ps"
      }
    }
  }

  post {
    success {
      echo 'Déploiement réussi'
    }
    failure {
      echo 'Oups, échec du pipeline'
    }
  }
}

