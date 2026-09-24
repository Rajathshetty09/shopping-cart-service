pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = 'shopping-cart-app'
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                // Check out YOUR repository where docker-compose.yml lives
                git branch: 'main', url: 'https://github.com/Rajathshetty09/shopping-cart-service.git'
            }
        }

        stage('Build & Spin Up Containers') {
            steps {
                sh 'docker compose --project-name ${COMPOSE_PROJECT_NAME} down --remove-orphans'
                sh 'docker compose --project-name ${COMPOSE_PROJECT_NAME} up -d --build'
            }
        }

        stage('Health Check') {
            steps {
                sleep 10
                sh 'docker ps --filter name=shopping-cart-service'
            }
        }
    }

    post {
        always {
            sh 'docker image prune -f'
        }
    }
}
