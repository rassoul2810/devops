pipeline {
  agent any

  environment {
    COMPOSE_FILE = "docker-compose.yml"
    ENV_FILE = ".env"
  }

  stages {
    stage('Clone') {
      steps {
        echo '📥 Clonage du dépôt déjà fait automatiquement.'
      }
    }

    stage('Stop containers') {
      steps {
        echo '🛑 Arrêt des conteneurs existants...'
        sh 'docker-compose -f ${COMPOSE_FILE} --env-file ${ENV_FILE} down || true'
      }
    }

    stage('Build') {
      steps {
        echo '🏗️ Construction des conteneurs...'
        sh 'docker-compose -f ${COMPOSE_FILE} --env-file ${ENV_FILE} build'
      }
    }

    stage('Deploy') {
      steps {
        echo '🚀 Lancement des conteneurs...'
        sh 'docker-compose -f ${COMPOSE_FILE} --env-file ${ENV_FILE} up -d'
      }
    }

    stage('Check') {
      steps {
        echo '🔍 Vérification des services en cours...'
        sh 'docker-compose ps'
      }
    }
  }

  post {
    failure {
      echo '❌ Oups, échec du pipeline.'
    }
    success {
      echo '✅ Pipeline terminé avec succès !'
    }
  }
}

